---
title: "페더레이션에 대해 구성 된 tooa 갤러리 응용 프로그램에 로그인 aaaProblems 단일 로그온 | Microsoft Docs"
description: "SAML 기반 페더레이션 single sign on Azure ad에 대해 구성한 응용 프로그램에 로그인 할 경우 특정 오류 hello에 대 한 지침"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: ba20a4904860cf063967029cad33fb80f16e4956
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooa-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="333e2-103">페더레이션된 single sign-on에 대해 구성 된 tooa 갤러리 응용 프로그램에 로그인 하는 문제</span><span class="sxs-lookup"><span data-stu-id="333e2-103">Problems signing in tooa gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="333e2-104">tootroubleshoot 문제를 다음과 같이 Azure AD에서 tooverify hello 응용 프로그램 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-104">tootroubleshoot your problem, you need tooverify hello application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="333e2-105">Hello Azure AD 갤러리 응용 프로그램에 대 한 모든 hello 구성 단계를 따랐는지 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-105">You have followed all hello configuration steps for hello Azure AD gallery application.</span></span>

-   <span data-ttu-id="333e2-106">hello 식별자 및 AAD에서 구성 된 회신 URL은 hello 응용 프로그램의 예상 값 일치</span><span class="sxs-lookup"><span data-stu-id="333e2-106">hello Identifier and Reply URL configured in AAD match they expected values in hello application</span></span>

-   <span data-ttu-id="333e2-107">사용자가 toohello 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="333e2-107">You have assigned users toohello application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="333e2-108">응용 프로그램을 디렉터리에서 찾을 수 없습니다</span><span class="sxs-lookup"><span data-stu-id="333e2-108">Application not found in directory</span></span>

<span data-ttu-id="333e2-109">*오류 AADSTS70001: 응용 프로그램 식별자 'https://contoso.com' hello 디렉터리에 없습니다.*합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in hello directory*.</span></span>

<span data-ttu-id="333e2-110">**가능한 원인**</span><span class="sxs-lookup"><span data-stu-id="333e2-110">**Possible cause**</span></span>

<span data-ttu-id="333e2-111">hello 발급자 특성 hello SAML 요청에는 AD hello Azure AD 응용 프로그램에 구성 된 hello 식별자 값과 일치 하지 않습니다 hello 응용 프로그램 tooAzure에서 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-111">hello Issuer attribute sends from hello application tooAzure AD in hello SAML request doesn’t match hello Identifier value configured in hello application Azure AD.</span></span>

<span data-ttu-id="333e2-112">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="333e2-112">**Resolution**</span></span>

<span data-ttu-id="333e2-113">Azure AD에서 구성 된 식별자 값 hello를 일치 하는 hello SAML 요청에서 해당 hello 발급자 특성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-113">Ensure that hello Issuer attribute in hello SAML request it’s matching hello Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="333e2-114">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="333e2-114">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="333e2-115">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-115">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="333e2-116">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-116">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="333e2-117">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-117">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="333e2-118">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-118">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="333e2-119">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="333e2-119">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="333e2-120">Hello 응용 프로그램 선택 tooconfigure single sign on</span><span class="sxs-lookup"><span data-stu-id="333e2-120">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="333e2-121">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-121">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="333e2-122">너무 이동**도메인 및 Url** 섹션.</span><span class="sxs-lookup"><span data-stu-id="333e2-122">Go too**Domain and URLs** section.</span></span> <span data-ttu-id="333e2-123">Hello 텍스트 상자에는 hello 오류가 표시 되는 hello 식별자 값에 대 한 hello 값과 일치 하는 식별자에에서 hello 값을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-123">Verify that hello value in hello Identifier textbox is matching hello value for hello identifier value displayed in hello error.</span></span>

<span data-ttu-id="333e2-124">Azure AD의 hello 식별자 값을 업데이트 한 후 해당 일치 하는 hello 값 hello SAML 요청에서 hello 응용 프로그램으로 전송 수 toosign toohello 응용 프로그램에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-124">After you have updated hello Identifier value in Azure AD and it’s matching hello value sends by hello application in hello SAML request, you should be able toosign in toohello application.</span></span>

## <a name="hello-reply-address-does-not-match-hello-reply-addresses-configured-for-hello-application"></a><span data-ttu-id="333e2-125">hello 회신 주소 hello 응용 프로그램으로 구성 된 hello 회신 주소를 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-125">hello reply address does not match hello reply addresses configured for hello application.</span></span>

<span data-ttu-id="333e2-126">*오류 AADSTS50011: hello 회신 주소 'https://contoso.com' hello 응용 프로그램으로 구성 된 hello 회신 주소를 일치 하지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="333e2-126">*Error AADSTS50011: hello reply address ‘https://contoso.com’ does not match hello reply addresses configured for hello application*</span></span>

<span data-ttu-id="333e2-127">**가능한 원인**</span><span class="sxs-lookup"><span data-stu-id="333e2-127">**Possible cause**</span></span>

<span data-ttu-id="333e2-128">hello hello SAML 요청에 AssertionConsumerServiceURL 값 hello 회신 URL 값 또는 Azure AD에 구성 된 패턴과 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-128">hello AssertionConsumerServiceURL value in hello SAML request doesn't match hello Reply URL value or pattern configured in Azure AD.</span></span> <span data-ttu-id="333e2-129">hello AssertionConsumerServiceURL hello SAML 요청에는 값은 hello 오류에서 참조 하는 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-129">hello AssertionConsumerServiceURL value in hello SAML request is hello URL you see in hello error.</span></span>

<span data-ttu-id="333e2-130">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="333e2-130">**Resolution**</span></span>

<span data-ttu-id="333e2-131">Azure AD에서의 일치 하는 hello 회신 URL 값 구성 hello SAML 요청에 hello AssertionConsumerServiceURL 값을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-131">Ensure that hello AssertionConsumerServiceURL value in hello SAML request it's matching hello Reply URL value configured in Azure AD.</span></span>

1.  <span data-ttu-id="333e2-132">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="333e2-132">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="333e2-133">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-133">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="333e2-134">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-134">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="333e2-135">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-135">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="333e2-136">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-136">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="333e2-137">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="333e2-137">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="333e2-138">Hello 응용 프로그램 선택 tooconfigure single sign on</span><span class="sxs-lookup"><span data-stu-id="333e2-138">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="333e2-139">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-139">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="333e2-140">너무 이동**도메인 및 Url** 섹션.</span><span class="sxs-lookup"><span data-stu-id="333e2-140">Go too**Domain and URLs** section.</span></span> <span data-ttu-id="333e2-141">확인 하거나 hello 회신 URL 텍스트 상자에 붙여넣습니다 toomatch hello hello SAML 요청에 AssertionConsumerServiceURL 값 hello 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-141">Verify or update hello value in hello Reply URL textbox toomatch hello AssertionConsumerServiceURL value in hello SAML request.</span></span>  
    * <span data-ttu-id="333e2-142">Hello 회신 URL 텍스트 상자에 표시 되지 않으면, 선택 hello **고급 URL 설정 표시** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-142">If you don't see hello Reply URL textbox, select hello **Show advanced URL settings** checkbox.</span></span>

<span data-ttu-id="333e2-143">Azure AD에서 hello 회신 URL 값을 업데이트 하 고 있으며 후 hello 값과 일치 하 hello 응용 프로그램에 의해 hello에서 SAML 요청을 보냅니다 수 toosign toohello 응용 프로그램에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-143">After you have updated hello Reply URL value in Azure AD and it’s matching hello value sends by hello application in hello SAML request, you should be able toosign in toohello application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="333e2-144">역할이 지정되지 않은 사용자</span><span class="sxs-lookup"><span data-stu-id="333e2-144">User not assigned a role</span></span>

<span data-ttu-id="333e2-145">*오류 AADSTS50105: 사용자에서 로그인 되었습니다. hello 'brian@contoso.com' hello 응용 프로그램에 대 한 tooa 역할 할당 되지 않은*합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-145">*Error AADSTS50105: hello signed in user 'brian@contoso.com' is not assigned tooa role for hello application*.</span></span>

<span data-ttu-id="333e2-146">**가능한 원인**</span><span class="sxs-lookup"><span data-stu-id="333e2-146">**Possible cause**</span></span>

<span data-ttu-id="333e2-147">hello 사용자는 액세스 toohello 응용 프로그램이 Azure AD에서 허가 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-147">hello user has not been granted access toohello application in Azure AD.</span></span>

<span data-ttu-id="333e2-148">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="333e2-148">**Resolution**</span></span>

<span data-ttu-id="333e2-149">tooassign 아래의 hello 단계를 직접 수행 하는 하나 이상의 사용자가 tooan 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="333e2-149">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="333e2-150">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="333e2-150">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="333e2-151">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-151">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="333e2-152">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-152">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="333e2-153">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-153">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="333e2-154">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-154">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="333e2-155">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="333e2-155">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="333e2-156">원하는 사용자 toofrom hello 목록 tooassign hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-156">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="333e2-157">Hello 응용 프로그램 로드 되 면 클릭 **사용자 및 그룹** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-157">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="333e2-158">Hello 클릭 **추가** hello 위로 단추 **사용자 및 그룹** 목록 tooopen hello **할당 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-158">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="333e2-159">hello 클릭 **사용자 및 그룹** hello에서 선택기 **할당 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-159">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="333e2-160">Hello 입력 **전체 이름** 또는 **전자 메일 주소** hello에 할당 하려는 hello 사용자의 **이름 또는 전자 메일 주소로 검색을 통해** 검색 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-160">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="333e2-161">Hello 위로 마우스를 가져가고 **사용자** hello 목록 tooreveal에는 **확인란**합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-161">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="333e2-162">Hello 확인란 다음 toohello 사용자의 프로필 사진 또는 로고 tooadd 사용자 toohello 클릭 **선택한** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-162">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="333e2-163">**선택 사항:** 너무 원하는 경우**둘 이상의 사용자를 추가**, 다른 유형 **전체 이름** 또는 **전자 메일 주소** hello에 **이름으로 검색 전자 메일 주소 또는** 상자에서 검색 하 고이 사용자 toohello hello 확인란 tooadd 클릭 **선택한** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-163">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="333e2-164">사용자 선택을 완료 했으면 클릭 hello **선택** 단추 tooadd 해당 사용자 및 그룹 toobe toohello 목록이 toohello 응용 프로그램을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-164">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="333e2-165">**선택 사항:** hello 클릭 **역할 선택** hello에 선택 기가 **할당 추가** 블레이드 tooselect 역할 tooassign toohello 사용자가 선택한 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-165">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="333e2-166">Hello 클릭 **할당** 단추 tooassign hello 응용 프로그램 toohello 사용자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-166">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="333e2-167">시간의 짧은 기간 이후에 hello 사용자가 선택한 이러한 응용 프로그램을 사용 하 여 hello hello 솔루션 설명 섹션에 설명 된 방법 수 toolaunch 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-167">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="333e2-168">유효한 SAML 요청이 아님</span><span class="sxs-lookup"><span data-stu-id="333e2-168">Not a valid SAML Request</span></span>

<span data-ttu-id="333e2-169">*오류 AADSTS75005: hello 요청을 유효한 토큰이 Saml2 프로토콜 메시지가 아닙니다.*</span><span class="sxs-lookup"><span data-stu-id="333e2-169">*Error AADSTS75005: hello request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="333e2-170">**가능한 원인**</span><span class="sxs-lookup"><span data-stu-id="333e2-170">**Possible cause**</span></span>

<span data-ttu-id="333e2-171">Azure AD SAML Single Sign on에 대 한 hello 응용 프로그램에서 보낸 요청 hello를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-171">Azure AD doesn’t support hello SAML Request sent by hello application for Single Sign-on.</span></span> <span data-ttu-id="333e2-172">일반적인 문제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-172">Some common issues are:</span></span>

-   <span data-ttu-id="333e2-173">Hello SAML 요청에 필수 필드가 누락</span><span class="sxs-lookup"><span data-stu-id="333e2-173">Missing required fields in hello SAML request</span></span>

-   <span data-ttu-id="333e2-174">SAML 요청 인코딩 방법</span><span class="sxs-lookup"><span data-stu-id="333e2-174">SAML request encoded method</span></span>

<span data-ttu-id="333e2-175">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="333e2-175">**Resolution**</span></span>

1.  <span data-ttu-id="333e2-176">SAML 요청을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-176">Capture SAML request.</span></span> <span data-ttu-id="333e2-177">hello 자습서에 따라 [어떻게 toodebug SAML 기반 single sign on tooapplications Azure AD에서](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toocapture hello SAML 요청 하는 방법을 toolearn 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-177">follow hello tutorial [How toodebug SAML-based single sign-on tooapplications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn how toocapture hello SAML request.</span></span>

2.  <span data-ttu-id="333e2-178">Hello 응용 프로그램 공급 업체와 공유 문의:</span><span class="sxs-lookup"><span data-stu-id="333e2-178">Contact hello application vendor and share:</span></span>

   -   <span data-ttu-id="333e2-179">SAML 요청</span><span class="sxs-lookup"><span data-stu-id="333e2-179">SAML request</span></span>

   -   [<span data-ttu-id="333e2-180">Azure AD Single Sign-On SAML 프로토콜 요구 사항</span><span class="sxs-lookup"><span data-stu-id="333e2-180">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="333e2-181">유효성을 검사 해야 Single Sign on에 대 한 hello Azure AD SAML 구현을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-181">They should validate they support hello Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="333e2-182">requiredResourceAccess 목록에 리소스 없음</span><span class="sxs-lookup"><span data-stu-id="333e2-182">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="333e2-183">*오류 AADSTS65005:hello 클라이언트 응용 프로그램에서 액세스 tooresource를 요청 하는 ' 00000002-0000-0000-c000-000000000000'. 이 요청이 실패 했습니다 hello 클라이언트가 requiredResourceAccess 목록에이 리소스를 지정 하지 않은*합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-183">*Error AADSTS65005:hello client application has requested access tooresource '00000002-0000-0000-c000-000000000000'. This request has failed because hello client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="333e2-184">**가능한 원인**</span><span class="sxs-lookup"><span data-stu-id="333e2-184">**Possible cause**</span></span>

<span data-ttu-id="333e2-185">hello application 개체 손상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-185">hello application object is corrupted.</span></span>

<span data-ttu-id="333e2-186">**해결 방법: 옵션 1**</span><span class="sxs-lookup"><span data-stu-id="333e2-186">**Resolution: option 1**</span></span>

<span data-ttu-id="333e2-187">toosolve hello 문제 hello Azure AD 구성에 hello 고유 식별자 값을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-187">toosolve hello problem, add hello unique Identifier value in hello Azure AD configuration.</span></span> <span data-ttu-id="333e2-188">아래의 hello 단계를 수행 하는 Id 값을 tooadd:</span><span class="sxs-lookup"><span data-stu-id="333e2-188">tooadd a Identifier value, follow hello steps below:</span></span>

1.  <span data-ttu-id="333e2-189">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="333e2-189">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="333e2-190">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-190">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="333e2-191">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-191">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="333e2-192">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-192">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="333e2-193">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-193">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="333e2-194">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="333e2-194">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="333e2-195">Single sign on 구성한 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-195">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="333e2-196">Hello 응용 프로그램 로드 되 면 hello 클릭 **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서</span><span class="sxs-lookup"><span data-stu-id="333e2-196">Once hello application loads, click on hello **Single sign-on** from hello application’s left hand navigation menu</span></span>

8.  <span data-ttu-id="333e2-197">Hello에서 **도메인 및 URL** 섹션에서 hello 확인 **고급 URL 설정 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-197">Under hello **Domain and URL** section, check on hello **Show advanced URL settings**.</span></span>

9.  <span data-ttu-id="333e2-198">hello에 **식별자** hello 응용 프로그램에 대 한 고유 식별자를 입력 하는 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-198">in hello **Identifier** textbox type a unique identifier for hello application.</span></span>

10. <span data-ttu-id="333e2-199">**저장** hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-199">**Save** hello configuration.</span></span>


<span data-ttu-id="333e2-200">**해결 방법: 옵션 2**</span><span class="sxs-lookup"><span data-stu-id="333e2-200">**Resolution option 2**</span></span>

<span data-ttu-id="333e2-201">위의 옵션 1으로 문제가 해결 되지 hello 디렉터리에서 hello 응용 프로그램을 제거 하십시오.</span><span class="sxs-lookup"><span data-stu-id="333e2-201">If option 1 above did not work for you, try removing hello application from hello directory.</span></span> <span data-ttu-id="333e2-202">그런 다음 추가 하 고 hello 응용 프로그램을 다시 구성 다음 hello 단계를 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="333e2-202">Then, add and reconfigure hello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="333e2-203">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="333e2-203">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="333e2-204">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-204">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="333e2-205">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-205">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="333e2-206">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-206">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="333e2-207">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-207">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="333e2-208">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="333e2-208">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="333e2-209">Hello 응용 프로그램 선택 tooconfigure single sign on</span><span class="sxs-lookup"><span data-stu-id="333e2-209">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="333e2-210">클릭 **삭제** hello의 왼쪽 위에 hello 응용 프로그램에서 **개요** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-210">Click **Delete** at hello top-left of hello application **Overview** blade.</span></span>

8.  <span data-ttu-id="333e2-211">Azure AD 새로 고치고 hello Azure AD 갤러리에서 hello 응용 프로그램을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-211">Refresh Azure AD and Add hello application from hello Azure AD gallery.</span></span> <span data-ttu-id="333e2-212">그런 다음 hello 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="333e2-212">Then, Configure hello application</span></span>

<span data-ttu-id="333e2-213"><span id="_Hlk477190176" class="anchor"></span>Hello 응용 프로그램을 다시 구성한 후 수 toosign toohello 응용 프로그램에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-213"><span id="_Hlk477190176" class="anchor"></span>After reconfiguring hello application, you should be able toosign in toohello application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="333e2-214">인증서 또는 키가 구성되지 않음</span><span class="sxs-lookup"><span data-stu-id="333e2-214">Certificate or key not configured</span></span>

<span data-ttu-id="333e2-215">*오류 AADSTS50003: 서명 키가 구성되지 않았습니다.*</span><span class="sxs-lookup"><span data-stu-id="333e2-215">*Error AADSTS50003: No signing key configured.*</span></span>

<span data-ttu-id="333e2-216">**가능한 원인**</span><span class="sxs-lookup"><span data-stu-id="333e2-216">**Possible cause**</span></span>

<span data-ttu-id="333e2-217">hello application 개체 손상 및 Azure AD는 hello 응용 프로그램에 대해 구성 된 hello 인증서를 인식 하지 못하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-217">hello application object is corrupted and Azure AD doesn’t recognize hello certificate configured for hello application.</span></span>

<span data-ttu-id="333e2-218">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="333e2-218">**Resolution**</span></span>

<span data-ttu-id="333e2-219">toodelete 새 인증서를 만들 다음 hello 단계를 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="333e2-219">toodelete and create a new certificate, follow hello steps below:</span></span>

1.  <span data-ttu-id="333e2-220">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="333e2-220">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="333e2-221">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-221">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="333e2-222">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-222">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="333e2-223">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-223">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="333e2-224">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-224">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="333e2-225">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="333e2-225">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="333e2-226">Hello 응용 프로그램 선택 tooconfigure single sign on</span><span class="sxs-lookup"><span data-stu-id="333e2-226">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="333e2-227">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-227">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="333e2-228">클릭 **새 인증서 만들기** hello에서 **SAML 서명 인증서** 섹션.</span><span class="sxs-lookup"><span data-stu-id="333e2-228">click **Create new certificate** under hello **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="333e2-229">[만료 날짜]를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-229">Select Expiration date.</span></span> <span data-ttu-id="333e2-230">그런 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-230">Then, click **Save.**</span></span>

10. <span data-ttu-id="333e2-231">확인 **새 인증서를 활성화할** toooverride hello 활성 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-231">Check **Make new certificate active** toooverride hello active certificate.</span></span> <span data-ttu-id="333e2-232">클릭 **저장** hello hello 블레이드 위쪽에 tooactivate hello 롤오버 인증서를 수락 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-232">Then, click **Save** at hello top of hello blade and accept tooactivate hello rollover certificate.</span></span>

11. <span data-ttu-id="333e2-233">Hello에서 **SAML 서명 인증서** 섹션에서 클릭 **제거** tooremove hello **사용 안 함** 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-233">Under hello **SAML Signing Certificate** section, click **remove** tooremove hello **Unused** certificate.</span></span>

## <a name="problem-when-customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="333e2-234">문제 hello SAML 클레임을 사용자 지정할 때 전송 tooan 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="333e2-234">Problem when customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="333e2-235">toolearn toocustomize hello SAML 특성 클레임 전송 tooyour 응용 프로그램 참조 [Azure Active Directory에서 매핑을 클레임](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="333e2-235">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="333e2-236">다음 단계</span><span class="sxs-lookup"><span data-stu-id="333e2-236">Next steps</span></span>
[<span data-ttu-id="333e2-237">어떻게 toodebug SAML 기반 single sign on tooapplications Azure AD에서</span><span class="sxs-lookup"><span data-stu-id="333e2-237">How toodebug SAML-based single sign-on tooapplications in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging)
