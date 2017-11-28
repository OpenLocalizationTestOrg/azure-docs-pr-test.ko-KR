---
title: "자세히 알아보기: Azure AD SSPR | Microsoft Docs"
description: "Azure AD 셀프 서비스 암호 재설정 자세히 알아보기"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 618c5908-5bf6-4f0d-bf88-5168dfb28a88
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: c177192bbe69d179a25d174b06a0813ec28e2615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-password-reset-in-azure-ad-deep-dive"></a><span data-ttu-id="2230b-103">Azure AD에서 셀프 서비스 암호 재설정 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="2230b-103">Self-service password reset in Azure AD deep dive</span></span>

<span data-ttu-id="2230b-104">SSPR는 어떻게 작동하나요?</span><span class="sxs-lookup"><span data-stu-id="2230b-104">How does SSPR work?</span></span> <span data-ttu-id="2230b-105">Hello 인터페이스에서 해당 옵션 의미</span><span class="sxs-lookup"><span data-stu-id="2230b-105">What does that option mean in hello interface?</span></span> <span data-ttu-id="2230b-106">Azure AD 셀프 서비스 암호에 대 한 자세한 내용을 toofind 계속 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-106">Continue reading toofind out more about Azure AD self-service password reset.</span></span>

## <a name="how-does-hello-password-reset-portal-work"></a><span data-ttu-id="2230b-107">Hello 암호 포털 작업을 재설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="2230b-107">How does hello password reset portal work</span></span>

<span data-ttu-id="2230b-108">사용자가 암호 재설정 포털 toohello, toodetermine 워크플로 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-108">When a user navigates toohello password reset portal, a workflow is kicked off toodetermine:</span></span>

   * <span data-ttu-id="2230b-109">Hello 페이지 지역화 어떻게?</span><span class="sxs-lookup"><span data-stu-id="2230b-109">How should hello page be localized?</span></span>
   * <span data-ttu-id="2230b-110">Hello 사용자 계정이 유효</span><span class="sxs-lookup"><span data-stu-id="2230b-110">Is hello user account valid?</span></span>
   * <span data-ttu-id="2230b-111">어떤 조직 hello 사용자에 속하지?</span><span class="sxs-lookup"><span data-stu-id="2230b-111">What organization does hello user belong to?</span></span>
   * <span data-ttu-id="2230b-112">여기서 hello 사용자의 암호 관리 되는지 여부</span><span class="sxs-lookup"><span data-stu-id="2230b-112">Where hello user’s password is managed?</span></span>
   * <span data-ttu-id="2230b-113">hello 사용자 사용이 허가 된 toouse hello 기능이입니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-113">Is hello user licensed toouse hello feature?</span></span>


<span data-ttu-id="2230b-114">Hello 암호 재설정 페이지 뒤에 있는 hello 논리에 대 한 toolearn 아래 hello 단계를 자세히 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-114">Read through hello steps below toolearn about hello logic behind hello password reset page.</span></span>

1. <span data-ttu-id="2230b-115">사용자가 클릭 hello 계정 링크에 액세스할 수 없거나 너무 라인 직접[https://passwordreset.microsoftonline.com](https://passwordreset.microsoftonline.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-115">User clicks hello Can’t access your account link or goes directly too[https://passwordreset.microsoftonline.com](https://passwordreset.microsoftonline.com).</span></span>
2. <span data-ttu-id="2230b-116">기반 hello 브라우저 로캘 hello 경험 hello 적절 한 언어로 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-116">Based on hello browser locale hello experience is rendered in hello appropriate language.</span></span> <span data-ttu-id="2230b-117">hello 암호 재설정 환경 언어로 지역화 하는 Office 365에서 지 원하는 동일한 언어를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-117">hello password reset experience is localized into hello same languages as Office 365 supports.</span></span>
3. <span data-ttu-id="2230b-118">사용자 ID를 입력하고 captcha를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-118">User enters a user id and passes a captcha.</span></span>
4. <span data-ttu-id="2230b-119">Azure AD hello 사용자 수 toouse 되는지 확인 hello 다음을 수행 하 여이 기능:</span><span class="sxs-lookup"><span data-stu-id="2230b-119">Azure AD verifies if hello user is able toouse this feature by doing hello following:</span></span>
   * <span data-ttu-id="2230b-120">hello이 사용자는이 기능은 설정 되 고 할당 된 Azure AD 라이선스를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-120">Checks that hello user has this feature enabled and an Azure AD license assigned.</span></span>
     * <span data-ttu-id="2230b-121">Hello 사용자가 없으면이 기능 사용 또는 라이선스가 할당 하는 경우 hello 사용자는 자신의 관리자 tooreset toocontact 요청 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-121">If hello user does not have this feature enabled or a license assigned, hello user is asked toocontact their administrator tooreset their password.</span></span>
   * <span data-ttu-id="2230b-122">해당 hello 사용자에 게 관리자 정책에 따라 자신의 계정에 정의 된 hello 오른쪽 인증 데이터를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-122">Checks that hello user has hello right challenge data defined on their account in accordance with administrator policy.</span></span>
     * <span data-ttu-id="2230b-123">정책에 하나의 인증만 필요한 경우 확인는 hello이 사용자는 hello 관리자 정책에서 사용 하는 hello 과제 중 하나 이상에 대해 정의 된 hello 적절 한 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-123">If policy requires only one challenge, then it is ensured that hello user has hello appropriate data defined for at least one of hello challenges enabled by hello administrator policy.</span></span>
       * <span data-ttu-id="2230b-124">Hello 사용자가 구성 되지 않은 사용자 hello 없으면이 권장된 toocontact 자신의 관리자 tooreset를는 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-124">If hello user is not configured, then hello user is advised toocontact their administrator tooreset their password.</span></span>
     * <span data-ttu-id="2230b-125">Hello 정책 두 개의 인증이 필요한 경우 확인는 hello이 사용자는 hello 관리자 정책에서 사용 하는 hello 과제 중 적어도 두 개에 대해 정의 된 hello 적절 한 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-125">If hello policy requires two challenges, then it is ensured that hello user has hello appropriate data defined for at least two of hello challenges enabled by hello administrator policy.</span></span>
       * <span data-ttu-id="2230b-126">Hello 사용자 구성 되지 않은 경우 사용자 hello 것이 권장된 toocontact 자신의 관리자 tooreset가 자신의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-126">If hello user is not configured, then we hello user is advised toocontact their administrator tooreset their password.</span></span>
   * <span data-ttu-id="2230b-127">Hello 사용자 암호가 온-프레미스 (페더레이션 또는 암호 해시 동기화)에서 관리 하는 경우를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-127">Checks if hello user’s password is managed on premises (federated or password hash synchronized).</span></span>
     * <span data-ttu-id="2230b-128">쓰기 저장이 배포 된 hello 사용자 암호가 온-프레미스에서 관리 되는 경우 hello 사용자 tooproceed tooauthenticate ï ´ ù 및 암호를 재설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-128">If writeback is deployed and hello user’s password is managed on premises, then hello user is allowed tooproceed tooauthenticate and reset their password.</span></span>
     * <span data-ttu-id="2230b-129">쓰기 저장이 배포 되지 않은 및 hello 사용자 암호가 온-프레미스로 관리 되는 경우 hello 사용자는 자신의 관리자 tooreset toocontact 요청 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-129">If writeback is not deployed and hello user’s password is managed on premises, then hello user is asked toocontact their administrator tooreset their password.</span></span>
5. <span data-ttu-id="2230b-130">해당 hello 사용자 수는 확인 되는 경우 toosuccessfully 암호를 재설정 한 후 hello 사용자 hello 재설정 프로세스가 안내 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-130">If it is determined that hello user is able toosuccessfully reset their password, then hello user is guided through hello reset process.</span></span>

## <a name="authentication-methods"></a><span data-ttu-id="2230b-131">인증 방법</span><span class="sxs-lookup"><span data-stu-id="2230b-131">Authentication methods</span></span>

<span data-ttu-id="2230b-132">셀프 서비스 암호 재설정 (SSPR)를 사용 하는 hello 다음 인증 방법에 대 한 옵션 중 하나 이상을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-132">If Self-Service Password Reset (SSPR) is enabled, you must select at least one of hello following options for authentication methods.</span></span> <span data-ttu-id="2230b-133">사용자가 더 유연하게 사용할 수 있도록 두 개 이상의 인증 방법을 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-133">We highly recommend choosing at least two authentication methods so that your users have more flexibility.</span></span>

* <span data-ttu-id="2230b-134">Email</span><span class="sxs-lookup"><span data-stu-id="2230b-134">Email</span></span>
* <span data-ttu-id="2230b-135">휴대폰</span><span class="sxs-lookup"><span data-stu-id="2230b-135">Mobile Phone</span></span>
* <span data-ttu-id="2230b-136">사무실 전화</span><span class="sxs-lookup"><span data-stu-id="2230b-136">Office Phone</span></span>
* <span data-ttu-id="2230b-137">Security Questions(보안 질문)</span><span class="sxs-lookup"><span data-stu-id="2230b-137">Security Questions</span></span>

### <a name="what-fields-are-used-in-hello-directory-for-authentication-data"></a><span data-ttu-id="2230b-138">인증 데이터에 대 한 hello 디렉터리 어떤 필드가 사용</span><span class="sxs-lookup"><span data-stu-id="2230b-138">What fields are used in hello directory for authentication data</span></span>

* <span data-ttu-id="2230b-139">사무실 전화에 전화 tooOffice 해당</span><span class="sxs-lookup"><span data-stu-id="2230b-139">Office Phone corresponds tooOffice Phone</span></span>
    * <span data-ttu-id="2230b-140">사용자가이 필드는 관리자가 정의 되어야 자체 수 없습니다 tooset</span><span class="sxs-lookup"><span data-stu-id="2230b-140">Users are unable tooset this field themselves it must be defined by an administrator</span></span>
* <span data-ttu-id="2230b-141">휴대폰 해당 tooeither 인증 전화 (공개적으로 볼 수 없음) 또는 휴대폰 (공개적으로 표시 됨)</span><span class="sxs-lookup"><span data-stu-id="2230b-141">Mobile Phone corresponds tooeither Authentication Phone (not publicly visible) or Mobile Phone (publicly visible)</span></span>
    * <span data-ttu-id="2230b-142">hello 서비스 인증 전화를 먼저 찾습니다, 그리고 다음 대체 전화 tooMobile 없는 경우</span><span class="sxs-lookup"><span data-stu-id="2230b-142">hello service looks for Authentication Phone first, then falls back tooMobile Phone if not present</span></span>
* <span data-ttu-id="2230b-143">Tooeither 인증 전자 메일 (공개적으로 볼 수 없음) 또는 대체 전자 메일을 해당 하는 대체 전자 메일 주소</span><span class="sxs-lookup"><span data-stu-id="2230b-143">Alternate Email Address corresponds tooeither Authentication Email (not publicly visible) or Alternate Email</span></span>
    * <span data-ttu-id="2230b-144">hello 서비스 인증 전자 메일을 먼저, 찾습니다 백 tooAlternate 전자 메일은 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-144">hello service looks for Authentication Email first, then fails back tooAlternate Email</span></span>

<span data-ttu-id="2230b-145">기본적으로만 hello 클라우드 특성 사무실 전화 및 이동 전화 인증 데이터에 대 한 온-프레미스 디렉터리에서 tooyour 클라우드 디렉터리를 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-145">By default, only hello cloud attributes Office Phone and Mobile Phone are synchronized tooyour cloud directory from your on-premises directory for authentication data.</span></span>

<span data-ttu-id="2230b-146">사용자가 암호 관리자에 게 해당 인증 방법의 hello 있는 데이터가 있는 경우 사용 하도록 설정한만 재설정 수 및 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-146">Users can only reset their password if they have data present in hello authentication methods that hello administrator has enabled and requires.</span></span>

<span data-ttu-id="2230b-147">사용자가 원하지 않는 자신의 휴대폰 번호 toobe hello 디렉터리에 표시 되지만 여전히 toouse 같은 것 암호 재설정을 위해 관리자 해야 하지 hello 디렉터리에 고 채우고 hello 사용자 채워야 다음 자신의 **인증 전화**  hello 통해 특성 [암호 재설정 등록 포털](http://aka.ms/ssprsetup)합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-147">If users do not want their mobile phone number toobe visible in hello directory but would still like toouse it for password reset, administrators should not populate it in hello directory and hello user should then populate their **Authentication Phone** attribute via hello [password reset registration portal](http://aka.ms/ssprsetup).</span></span> <span data-ttu-id="2230b-148">관리자 hello 사용자의 프로필에이 정보를 볼 수 있지만 다른 곳에서 게시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-148">Administrators can see this information in hello user's profile but it is not published elsewhere.</span></span> <span data-ttu-id="2230b-149">Azure 관리자 계정 인증 전화 번호를 등록 하면 hello 휴대폰 필드에 입력 하 고 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-149">If an Azure Administrator account registers their authentication phone number, it is populated into hello mobile phone field and is visible.</span></span>

### <a name="number-of-authentication-methods-required"></a><span data-ttu-id="2230b-150">필수 인증 방법의 수</span><span class="sxs-lookup"><span data-stu-id="2230b-150">Number of authentication methods required</span></span>

<span data-ttu-id="2230b-151">이 옵션 hello 최소 사용자 tooreset 거쳐야 hello 사용할 수 있는 인증 방법 수를 결정 합니다. 자신의 암호를 잠금 해제 하 고 tooeither 1 또는 2를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-151">This option determines hello minimum number of hello available authentication methods a user must go through tooreset or unlock their password and can be set tooeither 1 or 2.</span></span>

<span data-ttu-id="2230b-152">Hello 관리자가 설정 된 경우 사용자가 인증 방법을 더 toosupply 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-152">Users can choose toosupply more authentication methods if they are enabled by hello administrator.</span></span>

<span data-ttu-id="2230b-153">관리자 tooreset toorequest 안내 하는 오류 페이지를 참조 하 고 사용자에 필요한 최소 hello 메서드를 등록 하는 경우 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-153">If a user does not have hello minimum required methods registered, they see an error page that directs them toorequest an administrator tooreset their password.</span></span>

### <a name="how-secure-are-my-security-questions"></a><span data-ttu-id="2230b-154">보안 질문은 얼마나 안전한가요?</span><span class="sxs-lookup"><span data-stu-id="2230b-154">How secure are my security questions</span></span>

<span data-ttu-id="2230b-155">보안 질문을 사용 하는 경우 것이 좋습니다을 사용 중인 다른 메서드로 대로 어떤 사람들 hello 답변 tooanother 사용자 질문 알 수 있습니다 다른 방법 보다 보안 수준이 낮을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-155">If you use security questions, we recommend them in use with another method as they can be less secure than other methods since some people may know hello answers tooanother users questions.</span></span>

> [!NOTE] 
> <span data-ttu-id="2230b-156">보안 질문 hello 디렉터리에 사용자 개체에 비공개적으로 안전 하 게 저장 되 고 등록 하는 동안 사용자가 대답만 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-156">Security questions are stored privately and securely on a user object in hello directory and can only be answered by users during registration.</span></span> <span data-ttu-id="2230b-157">관리자 tooread에 대 한 방법이 있으면는 사용자가 수정 하거나 질문 또는 대답 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-157">There is no way for an administrator tooread or modify a users questions or answers.</span></span>
>

### <a name="security-question-localization"></a><span data-ttu-id="2230b-158">보안 질문 지역화</span><span class="sxs-lookup"><span data-stu-id="2230b-158">Security question localization</span></span>

<span data-ttu-id="2230b-159">다음에 나오는 모든 미리 정의 된 질문 hello 사용자의 브라우저 로캘을 기반으로 하는 Office 365 언어 중 일부만 hello로 지역화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-159">All predefined questions that follow are localized into hello full set of Office 365 languages based on hello user's browser locale.</span></span>

* <span data-ttu-id="2230b-160">배우자/파트너를 처음 만난 도시는 어디인가요?</span><span class="sxs-lookup"><span data-stu-id="2230b-160">In what city did you meet your first spouse/partner?</span></span>
* <span data-ttu-id="2230b-161">부모님이 처음 만난 도시는 어디인가요?</span><span class="sxs-lookup"><span data-stu-id="2230b-161">In what city did your parents meet?</span></span>
* <span data-ttu-id="2230b-162">가장 가까운 형제 자매가 사는 도시는 어디인가요?</span><span class="sxs-lookup"><span data-stu-id="2230b-162">In what city does your nearest sibling live?</span></span>
* <span data-ttu-id="2230b-163">아버지가 출생하신 도시는 어디인가요?</span><span class="sxs-lookup"><span data-stu-id="2230b-163">In what city was your father born?</span></span>
* <span data-ttu-id="2230b-164">첫 직장이 있는 도시는 어디인가요?</span><span class="sxs-lookup"><span data-stu-id="2230b-164">In what city was your first job?</span></span>
* <span data-ttu-id="2230b-165">어머니가 출생하신 도시는 어디인가요?</span><span class="sxs-lookup"><span data-stu-id="2230b-165">In what city was your mother born?</span></span>
* <span data-ttu-id="2230b-166">2000년에 새해를 맞은 도시는 어디인가요?</span><span class="sxs-lookup"><span data-stu-id="2230b-166">What city were you in on New Year's 2000?</span></span>
* <span data-ttu-id="2230b-167">Hello 높은에서 가장 좋아하는 선생님의 성은 무엇입니까 * 학교?</span><span class="sxs-lookup"><span data-stu-id="2230b-167">What is hello last name of your favorite teacher in high * school?</span></span>
* <span data-ttu-id="2230b-168">Hello 적용 대학의 이름은 무엇입니까 toobut स ा?</span><span class="sxs-lookup"><span data-stu-id="2230b-168">What is hello name of a college you applied toobut didn't attend?</span></span>
* <span data-ttu-id="2230b-169">hello 검사가 있는 사용자 첫 번째 결혼 피로연 hello 이름은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="2230b-169">What is hello name of hello place in which you held your first wedding reception?</span></span>
* <span data-ttu-id="2230b-170">아버지의 중간 이름은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="2230b-170">What is your father's middle name?</span></span>
* <span data-ttu-id="2230b-171">가장 좋아하는 음식은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="2230b-171">What is your favorite food?</span></span>
* <span data-ttu-id="2230b-172">외할머니의 성함은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="2230b-172">What is your maternal grandmother's first and last name?</span></span>
* <span data-ttu-id="2230b-173">어머니의 중간 이름은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="2230b-173">What is your mother's middle name?</span></span>
* <span data-ttu-id="2230b-174">가장 손위인 형제 자매의 생년월일은 언제인가요?</span><span class="sxs-lookup"><span data-stu-id="2230b-174">What is your oldest sibling's birthday month and year?</span></span> <span data-ttu-id="2230b-175">(예: 1985년 11월)</span><span class="sxs-lookup"><span data-stu-id="2230b-175">(e.g. November 1985)</span></span>
* <span data-ttu-id="2230b-176">가장 손위인 형제 자매의 중간 이름은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="2230b-176">What is your oldest sibling's middle name?</span></span>
* <span data-ttu-id="2230b-177">친할아버지의 성함은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="2230b-177">What is your paternal grandfather's first and last name?</span></span>
* <span data-ttu-id="2230b-178">가장 손아래인 형제 자매의 중간 이름은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="2230b-178">What is your youngest sibling's middle name?</span></span>
* <span data-ttu-id="2230b-179">6학년 때 다닌 학교는 어디인가요?</span><span class="sxs-lookup"><span data-stu-id="2230b-179">What school did you attend for sixth grade?</span></span>
* <span data-ttu-id="2230b-180">어떤 처음 hello च े 어린 시절 가장 친한 친구의 ं?</span><span class="sxs-lookup"><span data-stu-id="2230b-180">What was hello first and last name of your childhood best friend?</span></span>
* <span data-ttu-id="2230b-181">어떤 처음 hello च े 첫 번째 배우자의 ं?</span><span class="sxs-lookup"><span data-stu-id="2230b-181">What was hello first and last name of your first significant other?</span></span>
* <span data-ttu-id="2230b-182">hello 가장 좋아하는 초등학교 선생님의 성은 무엇 이었습니까?</span><span class="sxs-lookup"><span data-stu-id="2230b-182">What was hello last name of your favorite grade school teacher?</span></span>
* <span data-ttu-id="2230b-183">첫 번째 자동차 또는 오토바이의 hello 제조업체 및 모델 무엇 이었습니까?</span><span class="sxs-lookup"><span data-stu-id="2230b-183">What was hello make and model of your first car or motorcycle?</span></span>
* <span data-ttu-id="2230b-184">Hello 처음 다닌 학교의의 hello 이름은 무엇 이었습니까?</span><span class="sxs-lookup"><span data-stu-id="2230b-184">What was hello name of hello first school you attended?</span></span>
* <span data-ttu-id="2230b-185">태어난 hello 병원의 hello 이름은 무엇 이었습니까?</span><span class="sxs-lookup"><span data-stu-id="2230b-185">What was hello name of hello hospital in which you were born?</span></span>
* <span data-ttu-id="2230b-186">त ल ् ल े ं घ hello 이름을 hello?</span><span class="sxs-lookup"><span data-stu-id="2230b-186">What was hello name of hello street of your first childhood home?</span></span>
* <span data-ttu-id="2230b-187">어린 시절 영웅의 hello 이름은 무엇 이었습니까?</span><span class="sxs-lookup"><span data-stu-id="2230b-187">What was hello name of your childhood hero?</span></span>
* <span data-ttu-id="2230b-188">가장 좋아하는 봉 제 동물 인형의 hello 이름은 무엇 이었습니까?</span><span class="sxs-lookup"><span data-stu-id="2230b-188">What was hello name of your favorite stuffed animal?</span></span>
* <span data-ttu-id="2230b-189">첫 번째 애완 동물의 hello 이름은 무엇 이었습니까?</span><span class="sxs-lookup"><span data-stu-id="2230b-189">What was hello name of your first pet?</span></span>
* <span data-ttu-id="2230b-190">어린 시절 별명은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="2230b-190">What was your childhood nickname?</span></span>
* <span data-ttu-id="2230b-191">고등학교 때 가장 좋아한 스포츠는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="2230b-191">What was your favorite sport in high school?</span></span>
* <span data-ttu-id="2230b-192">첫 번째 직업은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="2230b-192">What was your first job?</span></span>
* <span data-ttu-id="2230b-193">어린 시절 전화 번호의 마지막 4 자리 hello 된 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="2230b-193">What were hello last four digits of your childhood telephone number?</span></span>
* <span data-ttu-id="2230b-194">त न ा, 무엇이 고 싶 었 toobe ज ा त?</span><span class="sxs-lookup"><span data-stu-id="2230b-194">When you were young, what did you want toobe when you grew up?</span></span>
* <span data-ttu-id="2230b-195">누구 hello ळ ् य ा가 입니까?</span><span class="sxs-lookup"><span data-stu-id="2230b-195">Who is hello most famous person you have ever met?</span></span>

### <a name="custom-security-questions"></a><span data-ttu-id="2230b-196">사용자 지정 보안 질문</span><span class="sxs-lookup"><span data-stu-id="2230b-196">Custom security questions</span></span>

<span data-ttu-id="2230b-197">사용자 지정 보안 질문은 여러 로캘로 지역화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-197">Custom security questions are not localized for different locales.</span></span> <span data-ttu-id="2230b-198">모든 사용자 지정 질문 hello에 표시 되는 hello 관리 사용자 인터페이스에 입력 된 hello 사용자의 브라우저 로캘 차이가 있는 경우에 동일한 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-198">All custom questions are displayed in hello same language they are entered in hello administrative user interface even if hello user's browser locale is different.</span></span> <span data-ttu-id="2230b-199">지역화 된 질문 해야 할 경우 미리 정의 된 hello 질문을 사용 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2230b-199">If you need localized questions, please use hello predefined questions.</span></span>

<span data-ttu-id="2230b-200">사용자 지정 보안 질문의 hello 최대 길이 200 자입니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-200">hello maximum length of a custom security question is 200 characters.</span></span>

### <a name="security-question-requirements"></a><span data-ttu-id="2230b-201">보안 질문 요구 사항</span><span class="sxs-lookup"><span data-stu-id="2230b-201">Security question requirements</span></span>

* <span data-ttu-id="2230b-202">최소 질문 문자 수 제한은 3자입니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-202">Minimum answer character limit is 3 characters</span></span>
* <span data-ttu-id="2230b-203">최대 질문 문자 수 제한은 40자입니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-203">Maximum answer character limit is 40 characters</span></span>
* <span data-ttu-id="2230b-204">사용자가 여러 번의 문을 제기 동일 hello 응답 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-204">Users may not answer hello same question more than one time</span></span>
* <span data-ttu-id="2230b-205">사용자가 hello를 제공 하지 않을 수 있습니다 하나 질문 보다 toomore 대답 동일</span><span class="sxs-lookup"><span data-stu-id="2230b-205">Users may not provide hello same answer toomore than one question</span></span>
* <span data-ttu-id="2230b-206">사용 되는 toodefine 질문 및 답변 유니코드 문자를 포함 하 여 모든 문자 집합 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-206">Any character set may be used toodefine questions and answers including Unicode characters</span></span>
* <span data-ttu-id="2230b-207">hello 정의 하는 질문 수보다 크거나 같아야 합니다 보다 큰 질문 필요한 tooregister toohello 수</span><span class="sxs-lookup"><span data-stu-id="2230b-207">hello number of questions defined must be greater than or equal toohello number of questions required tooregister</span></span>

## <a name="registration"></a><span data-ttu-id="2230b-208">등록</span><span class="sxs-lookup"><span data-stu-id="2230b-208">Registration</span></span>

### <a name="require-users-tooregister-when-signing-in"></a><span data-ttu-id="2230b-209">에 로그인 할 때 사용자가 tooregister 필요</span><span class="sxs-lookup"><span data-stu-id="2230b-209">Require users tooregister when signing in</span></span>

<span data-ttu-id="2230b-210">이 옵션을 사용 하면 사용자 암호를 사용할 수는 재설정 toocomplete hello 암호 재설정 등록에서 수행 하는 것과 같은 Azure AD toosign를 사용 하 여 tooapplications를 로그인 하는 경우 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-210">Enabling this option requires a user who is enabled for password reset toocomplete hello password reset registration if they login tooapplications using Azure AD toosign in like those that follow:</span></span>

* <span data-ttu-id="2230b-211">Office 365</span><span class="sxs-lookup"><span data-stu-id="2230b-211">Office 365</span></span>
* <span data-ttu-id="2230b-212">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="2230b-212">Azure portal</span></span>
* <span data-ttu-id="2230b-213">액세스 패널</span><span class="sxs-lookup"><span data-stu-id="2230b-213">Access Panel</span></span>
* <span data-ttu-id="2230b-214">페더레이션된 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2230b-214">Federated applications</span></span>
* <span data-ttu-id="2230b-215">Azure AD를 사용하여 응용 프로그램 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="2230b-215">Custom applications using Azure AD</span></span>

<span data-ttu-id="2230b-216">이 기능을 해제 하면 계속 사용자 toomanually 레지스터 그들의 연락처 정보 방문 하 여 [http://aka.ms/ssprsetup](http://aka.ms/ssprsetup) hello를 클릭 하 여 **암호 재설정에 등록할** hello 링크 hello 액세스 패널의 프로필 탭입니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-216">Disabling this feature will still allow users toomanually register their contact information by visiting [http://aka.ms/ssprsetup](http://aka.ms/ssprsetup) or by clicking hello **register for password reset** link under hello profile tab in hello access panel.</span></span>

> [!NOTE]
> <span data-ttu-id="2230b-217">사용자가 hello 창을 닫기 또는 취소를 클릭 하 여 hello 암호 재설정 등록 포털을 해제할 수 있지만 될 때마다 등록을 완료할 때까지 사용자가 로그인 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-217">Users can dismiss hello password reset registration portal by clicking cancel or closing hello window but are prompted each time they login until they complete registration.</span></span>
>

### <a name="number-of-days-before-users-are-asked-tooreconfirm-their-authentication-information"></a><span data-ttu-id="2230b-218">수 일 전에 사용자가 요청 tooreconfirm 해당 인증 정보</span><span class="sxs-lookup"><span data-stu-id="2230b-218">Number of days before users are asked tooreconfirm their authentication information</span></span>

<span data-ttu-id="2230b-219">이 옵션을 설정 하 고 인증 정보 reconfirming 사이의 hello 기간 결정 되며 hello를 사용 하는 경우 사용할 수만 **에 로그인 할 때 사용자가 tooregister 필요** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-219">This option determines hello period of time between setting and reconfirming authentication information and is only available if you enable hello **require users tooregister when signing in** option.</span></span>

<span data-ttu-id="2230b-220">유효한 값은 0-730 일 0 사용자 tooreconfirm 해당 인증 정보 묻지 않음</span><span class="sxs-lookup"><span data-stu-id="2230b-220">Valid values are 0-730 days with 0 meaning never ask users tooreconfirm their authentication information</span></span>

## <a name="notifications"></a><span data-ttu-id="2230b-221">알림</span><span class="sxs-lookup"><span data-stu-id="2230b-221">Notifications</span></span>

### <a name="notify-users-on-password-resets"></a><span data-ttu-id="2230b-222">사용자에게 암호 재설정에 대해 알림</span><span class="sxs-lookup"><span data-stu-id="2230b-222">Notify users on password resets</span></span>

<span data-ttu-id="2230b-223">이 옵션은 tooyes 설정, 그런 다음 hello 사용자가 암호를 재설정 하는 hello SSPR 포털 tootheir 주를 통해 해당 암호가 변경 되었습니다 및 대체 전자 메일을 파일에 Azure AD에서 해결 됨을 알리는 전자 메일을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-223">If this option is set tooyes, then hello user who is resetting their password receives an email notifying them that their password has been changed via hello SSPR portal tootheir primary and alternate email addresses on file in Azure AD.</span></span> <span data-ttu-id="2230b-224">누구도 이 재설정 이벤트의 알림을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-224">No one else is notified of this reset event.</span></span>

### <a name="notify-all-admins-when-other-admins-reset-their-passwords"></a><span data-ttu-id="2230b-225">다른 관리자가 암호를 재설정하면 모든 관리자에게 알림</span><span class="sxs-lookup"><span data-stu-id="2230b-225">Notify all admins when other admins reset their passwords</span></span>

<span data-ttu-id="2230b-226">이 옵션 설정 경우 tooyes, 다음 **모든 관리자** 다른 관리자가 SSPR을 사용 하 여 자신의 암호를 변경 된 것을 알리는 Azure AD에서 파일에 대해 전자 메일 tootheir 기본 전자 메일 주소를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-226">If this option is set tooyes, then **all administrators** receive an email tootheir primary email address on file in Azure AD notifying them that another administrator has changed their password using SSPR.</span></span>

<span data-ttu-id="2230b-227">예제: 환경에 4명의 관리자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-227">Example: There are four administrators in an environment.</span></span> <span data-ttu-id="2230b-228">관리자 "A"는 SSPR을 사용하여 해당 암호를 재설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-228">Administrator "A" resets their password using SSPR.</span></span> <span data-ttu-id="2230b-229">관리자 B, C 및 D는 이를 알리는 전자 메일을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-229">Administrators B, C, and D receive an email alerting them of this happening.</span></span>

## <a name="on-premises-integration"></a><span data-ttu-id="2230b-230">온-프레미스 통합</span><span class="sxs-lookup"><span data-stu-id="2230b-230">On-premises integration</span></span>

<span data-ttu-id="2230b-231">Azure AD Connect를 설치, 구성 및 사용하도록 설정하는 경우 온-프레미스 통합에 추가 옵션이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-231">If you have installed, configured, and enabled Azure AD Connect you will have additional options for on-premises integrations.</span></span>

### <a name="write-back-passwords-tooyour-on-premises-directory"></a><span data-ttu-id="2230b-232">암호 tooyour 온-프레미스 디렉터리 쓰기 저장</span><span class="sxs-lookup"><span data-stu-id="2230b-232">Write back passwords tooyour on-premises directory</span></span>

<span data-ttu-id="2230b-233">이 디렉터리에 대해 암호 쓰기 저장을 활성화 하는 지 여부를 제어 하 고 쓰기 저장에 있으면 hello 온-프레미스 쓰기 저장 서비스의 hello 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-233">Controls whether or not password writeback is enabled for this directory and, if writeback is on, indicates hello status of hello on-premises writeback service.</span></span> <span data-ttu-id="2230b-234">Azure AD Connect를 다시 구성 하지 않고 tootemporarily 사용 안 함 hello 암호 쓰기 저장을 원하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-234">This is useful if you want tootemporarily disable hello password writeback without re-configuring Azure AD Connect.</span></span>

* <span data-ttu-id="2230b-235">Hello 전환에 있으면 집합 tooyes 쓰기 저장 사용 하도록 설정 되며 페더레이션 및 암호 해시 동기화 사용자 수 tooreset 됩니다 암호.</span><span class="sxs-lookup"><span data-stu-id="2230b-235">If hello switch is set tooyes, then writeback will be enabled, and federated and password hash synchronized users will be able tooreset their passwords.</span></span>
* <span data-ttu-id="2230b-236">Hello 전환에 있으면 집합 toono 비활성화 되 고 페더레이션 쓰기 저장 및 암호 해시 동기화 사용자 수 tooreset 됩니다 암호.</span><span class="sxs-lookup"><span data-stu-id="2230b-236">If hello switch is set toono, then writeback will be disabled, and federated and password hash synchronized users will not be able tooreset their passwords.</span></span>

### <a name="allow-users-toounlock-accounts-without-resetting-their-password"></a><span data-ttu-id="2230b-237">사용자가 자신의 암호를 재설정 하지 않고 toounlock 계정 허용</span><span class="sxs-lookup"><span data-stu-id="2230b-237">Allow users toounlock accounts without resetting their password</span></span>

<span data-ttu-id="2230b-238">Hello 암호 재설정 포털을 방문 하는 사용자가 암호를 재설정 하지 않고 자신의 온-프레미스 Active Directory 계정 지정된 hello 옵션 toounlock 해야 하는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-238">Designates whether or not users who visit hello password reset portal should be given hello option toounlock their on-premises Active Directory accounts without resetting their password.</span></span> <span data-ttu-id="2230b-239">기본적으로 Azure AD는 항상 계정 잠금 해제 암호 재설정을 수행할 때,이 설정을 통해 tooseparate 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-239">By default, Azure AD will always unlock accounts when performing a password reset, this setting allows you tooseparate those two operations.</span></span> 

* <span data-ttu-id="2230b-240">경우 "yes" 사용자 지정된 hello 옵션 tooreset 암호 수를 hello 계정 또는 toounlock hello 암호를 재설정 하지 않고 잠금을 해제 한 후 너무 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-240">If set too“yes”, then users will be given hello option tooreset their password and unlock hello account, or toounlock without resetting hello password.</span></span>
* <span data-ttu-id="2230b-241">경우 설정 너무 "no" 인 사용자만 수 tooperform 됩니다 결합 된 암호 재설정 및 계정 잠금 해제 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-241">If set too“no”, then users will only be able tooperform a combined password reset and account unlock operation.</span></span>

## <a name="network-requirements"></a><span data-ttu-id="2230b-242">네트워크 요구 사항</span><span class="sxs-lookup"><span data-stu-id="2230b-242">Network requirements</span></span>

### <a name="firewall-rules"></a><span data-ttu-id="2230b-243">방화벽 규칙</span><span class="sxs-lookup"><span data-stu-id="2230b-243">Firewall rules</span></span>

[<span data-ttu-id="2230b-244">Microsoft Office URL 및 IP 주소 목록</span><span class="sxs-lookup"><span data-stu-id="2230b-244">List of Microsoft Office URLs and IP addresses</span></span>](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)

<span data-ttu-id="2230b-245">이상에서는 및 Azure AD Connect 1.1.443.0 버전에 대 한 아웃 바운드 HTTPS 액세스 toohello 다음 필요 하며</span><span class="sxs-lookup"><span data-stu-id="2230b-245">For Azure AD Connect version 1.1.443.0 and above, you need outbound HTTPS access toohello following</span></span>
* <span data-ttu-id="2230b-246">passwordreset.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="2230b-246">passwordreset.microsoftonline.com</span></span>
* <span data-ttu-id="2230b-247">servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="2230b-247">servicebus.windows.net</span></span>

<span data-ttu-id="2230b-248">보다 세부적인 액세스에 대 한 Microsoft Azure 데이터 센터 IP 범위 수요일 마다 업데이트 되어 효과 hello 다음에 배치 하는 hello 업데이트 목록을 찾을 수 있습니다 월요일 [여기](https://www.microsoft.com/download/details.aspx?id=41653)합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-248">For more granular access, you can find hello updated list of Microsoft Azure Datacenter IP Ranges that is updated every Wednesday and put into effect hello following Monday [here](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

### <a name="idle-connection-timeouts"></a><span data-ttu-id="2230b-249">유휴 연결 시간 제한</span><span class="sxs-lookup"><span data-stu-id="2230b-249">Idle connection timeouts</span></span>

<span data-ttu-id="2230b-250">hello Azure AD Connect 도구 주기적 ping/keepalives tooServiceBus 끝점 tooensure를 hello 연결 유지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-250">hello Azure AD Connect tool sends periodic pings/keepalives tooServiceBus endpoints tooensure that hello connections stay alive.</span></span> <span data-ttu-id="2230b-251">너무 많은 연결이 중지 되 고 됩니다 hello 도구 검색 해야, 것 ping toohello 끝점의 hello 주파수를 자동으로 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-251">Should hello tool detect that too many connections are being killed, it will automatically increase hello frequency of pings toohello endpoint.</span></span> <span data-ttu-id="2230b-252">그러나 hello 가장 낮은 '간격으로 ping' 삭제 toois 1 ping 60 초 마다 것이 좋습니다 프록시/방화벽 2-3 분 이상 유휴 연결 toopersist를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-252">hello lowest 'ping intervals' drops toois 1 ping every 60 seconds, however, we strongly advise that proxies/firewalls allow idle connections toopersist for at least 2-3 minutes.</span></span> <span data-ttu-id="2230b-253">*오래된 버전의 경우 4분 이상이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-253">*For older versions, we suggest four minutes or more.</span></span>

## <a name="active-directory-permissions"></a><span data-ttu-id="2230b-254">Active Directory 사용 권한</span><span class="sxs-lookup"><span data-stu-id="2230b-254">Active Directory permissions</span></span>

<span data-ttu-id="2230b-255">hello hello Azure AD Connect 유틸리티에 지정 된 계정이 있어야 암호 재설정 "," 암호 변경 "," lockoutTime에 대 한 쓰기 권한을 "및" pwdLastSet의 hello 루트 개체 중 하나에 대 한 권한 확장에 대 한 쓰기 권한을 **각 도메인** 해당 포리스트의 **또는** 원하는 범위 SSPR에 toobe hello 사용자 Ou에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-255">hello account specified in hello Azure AD Connect utility must have Reset Password, Change Password, Write Permissions on lockoutTime, and Write Permissions on pwdLastSet, extended rights on either hello root object of **each domain** in that forest **OR** on hello user OUs you wish toobe in scope for SSPR.</span></span>

<span data-ttu-id="2230b-256">확실 하지 않은 경우 위의 어떤 계정 hello hello Azure Active Directory Connect 구성 UI 열고 hello 현재 구성 옵션 보기를 클릭 합니다. 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-256">If you are not sure what account hello above refers to, open hello Azure Active Directory Connect configuration UI and click hello View current configuration option.</span></span> <span data-ttu-id="2230b-257">tooadd 권한 toois "디렉터리 동기화" 아래에 나열 해야 하는 hello 계정</span><span class="sxs-lookup"><span data-stu-id="2230b-257">hello account you need tooadd permission toois listed under "Synchronized Directories"</span></span>

<span data-ttu-id="2230b-258">사용자 계정 대신 하 여 hello MA 서비스 계정이 각 포리스트에 toomanage 암호에 대 한 해당 포리스트 내 허용 이러한 사용 권한을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-258">Setting these permissions allows hello MA service account for each forest toomanage passwords on behalf of user accounts within that forest.</span></span> <span data-ttu-id="2230b-259">**것을 잊은 경우 tooassign 이러한 사용 권한을 다음, 쓰기 저장 toobe 올바르게 구성 되어 나타나는 경우에, 사용자가 toomanage hello 클라우드에서 온-프레미스 암호를 시도할 때 오류가 발생 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2230b-259">**If you neglect tooassign these permissions, then, even though writeback appears toobe configured correctly, users encounter errors when attempting toomanage their on-premises passwords from hello cloud.**</span></span>

> [!NOTE]
> <span data-ttu-id="2230b-260">디렉터리의 이러한 사용 권한 tooreplicate tooall 개체에 대 한 tooan 시간 이상 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-260">It could take up tooan hour or more for these permissions tooreplicate tooall objects in your directory.</span></span>
>

<span data-ttu-id="2230b-261">암호 쓰기 저장 toooccur에 대 한 적절 한 권한을 hello tooset</span><span class="sxs-lookup"><span data-stu-id="2230b-261">tooset up hello appropriate permissions for password writeback toooccur</span></span>

1. <span data-ttu-id="2230b-262">Hello 적절 한 도메인 관리 권한이 있는 계정으로 Active Directory 사용자 및 컴퓨터를 열려면</span><span class="sxs-lookup"><span data-stu-id="2230b-262">Open Active Directory Users and Computers with an account that has hello appropriate domain administration permissions</span></span>
2. <span data-ttu-id="2230b-263">Hello 보기 메뉴에서 고급 기능 설정 되어 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="2230b-263">From hello View menu, make sure Advanced Features is turned on</span></span>
3. <span data-ttu-id="2230b-264">Hello 왼쪽된 패널에서 hello 도메인의 hello 루트를 나타내는 hello 개체를 마우스 오른쪽 단추로 클릭 하 고 속성 선택</span><span class="sxs-lookup"><span data-stu-id="2230b-264">In hello left panel, right-click hello object that represents hello root of hello domain and choose properties</span></span>
    * <span data-ttu-id="2230b-265">Hello 보안 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-265">Click hello Security tab</span></span>
    * <span data-ttu-id="2230b-266">[고급]을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-266">Then click Advanced.</span></span>
4. <span data-ttu-id="2230b-267">Hello 사용 권한 탭에서 추가 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-267">From hello Permissions tab, click Add</span></span>
5. <span data-ttu-id="2230b-268">사용 권한이 너무 (Azure AD Connect 설치 프로그램에서) 적용 되는 hello 계정 선택</span><span class="sxs-lookup"><span data-stu-id="2230b-268">Pick hello account that permissions are being applied too(from Azure AD Connect setup)</span></span>
6. <span data-ttu-id="2230b-269">Hello 적용 toodrop 상자에서 하위 사용자 개체를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-269">In hello Applies toodrop down box select Descendent User objects</span></span>
7. <span data-ttu-id="2230b-270">사용 권한 아래에서 확인란 hello hello 다음에 대 한</span><span class="sxs-lookup"><span data-stu-id="2230b-270">Under permissions check hello boxes for hello following</span></span>
    * <span data-ttu-id="2230b-271">암호 만료 안 됨</span><span class="sxs-lookup"><span data-stu-id="2230b-271">Unexpire-Password</span></span>
    * <span data-ttu-id="2230b-272">암호 재설정</span><span class="sxs-lookup"><span data-stu-id="2230b-272">Reset Password</span></span>
    * <span data-ttu-id="2230b-273">암호 변경</span><span class="sxs-lookup"><span data-stu-id="2230b-273">Change Password</span></span>
    * <span data-ttu-id="2230b-274">lockoutTime 쓰기</span><span class="sxs-lookup"><span data-stu-id="2230b-274">Write lockoutTime</span></span>
    * <span data-ttu-id="2230b-275">pwdLastSet 쓰기</span><span class="sxs-lookup"><span data-stu-id="2230b-275">Write pwdLastSet</span></span>
8. <span data-ttu-id="2230b-276">Tooapply를 통해 적용/확인을 클릭 하 고 열려 있는 대화 상자를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-276">Click Apply/OK through tooapply and exit any open dialog boxes.</span></span>

## <a name="how-does-password-reset-work-for-b2b-users"></a><span data-ttu-id="2230b-277">B2B 사용자에 대한 암호 재설정은 어떻게 작동하나요?</span><span class="sxs-lookup"><span data-stu-id="2230b-277">How does password reset work for B2B users?</span></span>
<span data-ttu-id="2230b-278">암호 재설정 및 변경은 모든 B2B 구성에서 완전히 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-278">Password reset and change are fully supported with all B2B configurations.</span></span>  <span data-ttu-id="2230b-279">Hello 세 명시적 B2B 경우 암호 재설정에서 지 원하는 아래를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-279">Read below for hello three explicit B2B cases supported by password reset.</span></span>

1. <span data-ttu-id="2230b-280">**기존 Azure AD 테 넌 트와 파트너 조직에서 사용자가** -와 협력 하는 hello 조직에 기존 Azure AD 테 넌 트에서는 **암호 재설정 정책을 해당 테 넌 트에 설정 된 존중**합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-280">**Users from a partner org with an existing Azure AD tenant** - If hello organization you are partnering with has an existing Azure AD tenant, we **respect whatever password reset policies are enabled in that tenant**.</span></span> <span data-ttu-id="2230b-281">단계를 hello 암호 재설정 toowork, 파트너 조직 정당한 요구 toomake Azure AD SSPR를 사용할 수 있는지는 O365 고객에 대 한 추가 비용 없이 hello 및 수행 하 여 사용 하도록 설정할 수 있습니다에 대 한 우리의 [암호 관리 시작 ](https://azure.microsoft.com/documentation/articles/active-directory-passwords-getting-started/#enable-users-to-reset-or-change-their-aad-passwords) 가이드입니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-281">For password reset toowork, hello partner organization just needs toomake sure Azure AD SSPR is enabled, which is no additional charge for O365 customers, and can be enabled by following hello steps in our [Getting Started with Password Management](https://azure.microsoft.com/documentation/articles/active-directory-passwords-getting-started/#enable-users-to-reset-or-change-their-aad-passwords) guide.</span></span>
2. <span data-ttu-id="2230b-282">**사용 하 여 등록 한 사용자 [셀프 서비스 등록](active-directory-self-service-signup.md)**  -와 협력 하는 hello 조직 hello를 사용 하는 경우 [셀프 서비스 등록](active-directory-self-service-signup.md) 테 넌 트에 기능 tooget, 우리 수 있도록 기본 설정으로 복원을 hello 등록 됩니까 전자 메일입니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-282">**Users who signed up using [self-service sign-up](active-directory-self-service-signup.md)** - If hello organization you are partnering with used hello [self-service sign-up](active-directory-self-service-signup.md) feature tooget into a tenant, we let them reset with hello email they registered.</span></span>
3. <span data-ttu-id="2230b-283">**B2B 사용자** -새 hello를 사용 하 여 만든 모든 새 B2B 사용자 [Azure AD B2B 기능](active-directory-b2b-what-is-azure-ad-b2b.md) 됩니다 수 tooreset hello 초대 프로세스 중에 등록 됩니까 hello 전자 메일을 가진 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-283">**B2B users** - Any new B2B users created using hello new [Azure AD B2B capabilities](active-directory-b2b-what-is-azure-ad-b2b.md) will also be able tooreset their passwords with hello email they registered during hello invite process.</span></span>

<span data-ttu-id="2230b-284">tootest 이동이, toohttp://passwordreset.microsoftonline.com 이러한 파트너 사용자 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-284">tootest this, go toohttp://passwordreset.microsoftonline.com with one of these partner users.</span></span> <span data-ttu-id="2230b-285">대체 전자 메일 또는 인증 전자 메일이 정의되어 있으면 암호 재설정이 예상대로 작동됩니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-285">As long as they have an alternate email or authentication email defined, password reset works as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2230b-286">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2230b-286">Next steps</span></span>

<span data-ttu-id="2230b-287">링크를 따라 hello Azure AD를 사용 하 여 다시 설정 하는 암호에 대 한 추가 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-287">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="2230b-288">[**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작</span><span class="sxs-lookup"><span data-stu-id="2230b-288">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="2230b-289">[**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성</span><span class="sxs-lookup"><span data-stu-id="2230b-289">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="2230b-290">[**데이터** ](active-directory-passwords-data.md) -hello 필요한 데이터를 이해 하 고 암호 관리에 대 한 사용 방법</span><span class="sxs-lookup"><span data-stu-id="2230b-290">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="2230b-291">[**롤아웃** ](active-directory-passwords-best-practices.md) -계획 및 배포 ´ ֿ ´ hello 지침을 사용 하 여 SSPR tooyour 사용자</span><span class="sxs-lookup"><span data-stu-id="2230b-291">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="2230b-292">[**정책**](active-directory-passwords-policy.md) - Azure AD 암호 정책을 이해하고 설정</span><span class="sxs-lookup"><span data-stu-id="2230b-292">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="2230b-293">[**비밀번호 쓰기 저장**](active-directory-passwords-writeback.md) - 비밀번호 쓰기 저장이 온-프레미스 디렉터리와 함께 작동 하는 원리</span><span class="sxs-lookup"><span data-stu-id="2230b-293">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="2230b-294">[**사용자 지정** ](active-directory-passwords-customize.md) -hello SSPR 귀사에 대 한 경험의 hello 모양과 느낌을 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2230b-294">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="2230b-295">[**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색</span><span class="sxs-lookup"><span data-stu-id="2230b-295">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="2230b-296">[**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로?</span><span class="sxs-lookup"><span data-stu-id="2230b-296">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="2230b-297">그 이유는</span><span class="sxs-lookup"><span data-stu-id="2230b-297">Why?</span></span> <span data-ttu-id="2230b-298">무엇을?</span><span class="sxs-lookup"><span data-stu-id="2230b-298">What?</span></span> <span data-ttu-id="2230b-299">어디서?</span><span class="sxs-lookup"><span data-stu-id="2230b-299">Where?</span></span> <span data-ttu-id="2230b-300">누가?</span><span class="sxs-lookup"><span data-stu-id="2230b-300">Who?</span></span> <span data-ttu-id="2230b-301">언제?</span><span class="sxs-lookup"><span data-stu-id="2230b-301">When?</span></span> <span data-ttu-id="2230b-302">-Tooask 항상 필요한 tooquestions 답변</span><span class="sxs-lookup"><span data-stu-id="2230b-302">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="2230b-303">[**문제를 해결** ](active-directory-passwords-troubleshoot.md) -SSPR으로 보면 tooresolve 공통을 발급 하는 방법에 대해 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="2230b-303">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>

