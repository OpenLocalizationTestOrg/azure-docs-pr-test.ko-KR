---
title: "single sign on 갤러리가 아닌 응용 프로그램에 대 한 페더레이션 aaaHow tooconfigure | Microsoft Docs"
description: "Single sign on Azure AD와 toointegrate 원하는 사용자 지정 갤러리 아닌 응용 프로그램에 대 한 tooconfigure 페더레이션 하는 방법"
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
ms.openlocfilehash: f4a37cb500c075d0ce917ad8f13411f2ce208c56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="3a3c2-103">Single sign on 갤러리가 아닌 응용 프로그램에 대 한 tooconfigure 페더레이션 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3a3c2-103">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="3a3c2-104">toohave Azure AD premium이 필요 tooconfigure 갤러리가 아닌 응용 프로그램 및 hello 응용 프로그램이 SAML 2.0을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-104">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="3a3c2-105">Azure AD 버전에 대한 자세한 내용은 [Azure AD 가격 책정](https://azure.microsoft.com/pricing/details/active-directory/)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-105">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="3a3c2-106">필요한 단계 개요</span><span class="sxs-lookup"><span data-stu-id="3a3c2-106">Overview of steps required</span></span>
<span data-ttu-id="3a3c2-107">아래 내용은 hello 단계 필요한 tooconfigure 페더레이션된 single sign-on의 갤러리 외에 대 한 높은 수준의 개요입니다 (예: 사용자 지정) 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-107">Below is a high level overview of hello steps required tooconfigure federated single sign-on for a non-gallery (e.g., custom) application.</span></span>

-   [<span data-ttu-id="3a3c2-108">Azure ad (로그온 URL, 식별자, 회신 URL) hello 응용 프로그램의 메타 데이터 값을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-108">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="3a3c2-109">사용자의 Id를 선택 하 고 사용자 특성 전송 toobe toohello 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="3a3c2-109">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="3a3c2-110">Azure AD 메타데이터 및 인증서 검색</span><span class="sxs-lookup"><span data-stu-id="3a3c2-110">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="3a3c2-111">Hello 응용 프로그램 (로그온 URL, 발급자, 로그 아웃 URL 및 인증서)에 Azure AD 메타 데이터 값을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-111">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="3a3c2-112">사용자가 toohello 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="3a3c2-112">Assign users toohello application</span></span>](#_Assign_users_to_the_application)

## <a name="configuring-single-sign-on-toonon-gallery-applications"></a><span data-ttu-id="3a3c2-113">Single sign on toonon-갤러리 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="3a3c2-113">Configuring single sign-on toonon-gallery applications</span></span>

<span data-ttu-id="3a3c2-114">tooconfigure single sign on hello Azure AD 갤러리에 없는 응용 프로그램에 대 한 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-114">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="3a3c2-115">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="3a3c2-115">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="3a3c2-116">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-116">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3a3c2-117">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-117">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3a3c2-118">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-118">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3a3c2-119">hello 클릭 **추가** hello hello 오른쪽 위 모서리에 있는 단추 **엔터프라이즈 응용 프로그램** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-119">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="3a3c2-120">클릭 **비 갤러리 응용 프로그램** hello에 **위해 자신의 앱 추가** 섹션</span><span class="sxs-lookup"><span data-stu-id="3a3c2-120">click **Non-gallery application** in hello **Add your own app** section</span></span>

7.  <span data-ttu-id="3a3c2-121">Hello에 hello 응용 프로그램의 hello 이름을 입력 **이름** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-121">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="3a3c2-122">클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-122">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="3a3c2-123">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-123">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="3a3c2-124">선택 **SAML 기반 로그온** hello에 **모드** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-124">Select **SAML-based Sign-on** in hello **Mode** dropdown.</span></span>

11. <span data-ttu-id="3a3c2-125">필요한 hello 값을 입력 **도메인 및 Url입니다.**</span><span class="sxs-lookup"><span data-stu-id="3a3c2-125">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="3a3c2-126">Hello 응용 프로그램 공급 업체에서 이러한 값을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-126">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="3a3c2-127">IdP에서 시작한 SSO와 tooconfigure hello 응용 프로그램 회신 URL hello 및 hello 식별자를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-127">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

   2. <span data-ttu-id="3a3c2-128">**선택 사항:** SP에서 시작한 SSO와 tooconfigure hello 응용 프로그램 hello 로그인 URL에 필요한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-128">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="3a3c2-129">Hello에 **사용자 특성**, 선택 hello에 있는 사용자에 대 한 고유 식별자를 hello **사용자 식별자** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-129">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="3a3c2-130">**선택 사항:** 클릭 **보기 및 다른 모든 사용자 특성 편집** tooedit hello 사용자가 로그인 할 때 hello SAML 토큰에서 보낸 toobe toohello 응용 프로그램 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-130">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="3a3c2-131">tooadd 특성:</span><span class="sxs-lookup"><span data-stu-id="3a3c2-131">tooadd an attribute:</span></span>

   1. <span data-ttu-id="3a3c2-132">**특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-132">click **Add attribute**.</span></span> <span data-ttu-id="3a3c2-133">Hello 입력 **이름** 및 hello 선택 hello **값** hello 드롭다운에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-133">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="3a3c2-134">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-134">Click **Save.**</span></span> <span data-ttu-id="3a3c2-135">Hello 테이블에 새 특성을 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-135">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="3a3c2-136">클릭 **구성 &lt;응용 프로그램 이름&gt;**  방법은 tooaccess 설명서 tooconfigure single sign on hello 응용 프로그램에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-136">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="3a3c2-137">또한 Azure AD Url 및 hello 응용 프로그램에 필요한 인증서에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-137">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

15. [<span data-ttu-id="3a3c2-138">Toohello 응용 프로그램 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-138">Assign users toohello application.</span></span>](#assign-users-to-the-application)

## <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="3a3c2-139">사용자의 Id를 선택 하 고 사용자 특성 전송 toobe toohello 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="3a3c2-139">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="3a3c2-140">tooselect hello 사용자 식별자 또는 사용자 특성 추가, 아래의 hello 단계를 수행:</span><span class="sxs-lookup"><span data-stu-id="3a3c2-140">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="3a3c2-141">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="3a3c2-141">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="3a3c2-142">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-142">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3a3c2-143">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-143">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3a3c2-144">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-144">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3a3c2-145">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-145">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="3a3c2-146">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="3a3c2-146">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="3a3c2-147">Single sign on 구성한 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-147">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="3a3c2-148">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-148">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3a3c2-149">Hello에서 **사용자 특성** 섹션에서 사용자 hello에 대 한 고유 식별자를 hello **사용자 식별자** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-149">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="3a3c2-150">hello 선택된 된 옵션 두어야 hello 응용 프로그램 tooauthenticate hello 사용자에서 toomatch hello 예상 값.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-150">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

 ><span data-ttu-id="3a3c2-151">[! 참고 (를) Azure AD 선택한 hello 값에 따라 hello NameID 특성 (사용자 식별자)에 대 한 hello 형식을 선택 하거나 SAML AuthRequest hello에 hello 응용 프로그램에서 요청한 형식 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-151">[!NOTE} Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="3a3c2-152">자세한 내용은 방문 hello 문서 [Single Sign On SAML 프로토콜](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) hello에서 NameIDPolicy 섹션.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-152">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
 >
 >

9.  <span data-ttu-id="3a3c2-153">tooadd 사용자 특성을 클릭 하 여 **보기 및 다른 모든 사용자 특성을 편집** tooedit hello 사용자가 로그인 할 때 hello SAML 토큰에서 보낸 toobe toohello 응용 프로그램 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-153">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="3a3c2-154">tooadd 특성:</span><span class="sxs-lookup"><span data-stu-id="3a3c2-154">tooadd an attribute:</span></span>

   1. <span data-ttu-id="3a3c2-155">**특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-155">click **Add attribute**.</span></span> <span data-ttu-id="3a3c2-156">Hello 입력 **이름** 및 hello 선택 hello **값** hello 드롭다운에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-156">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="3a3c2-157">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-157">Click **Save.**</span></span> <span data-ttu-id="3a3c2-158">Hello 테이블에 새 특성을 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-158">You see hello new attribute in hello table.</span></span>

## <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="3a3c2-159">Hello Azure AD 메타 데이터 또는 인증서를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-159">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="3a3c2-160">toodownload hello에 대 한 응용 프로그램 메타 데이터 또는 Azure AD에서 인증서를 다음 hello 단계를 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-160">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="3a3c2-161">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="3a3c2-161">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="3a3c2-162">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-162">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3a3c2-163">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-163">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3a3c2-164">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-164">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3a3c2-165">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-165">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="3a3c2-166">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="3a3c2-166">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="3a3c2-167">Single sign on 구성한 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-167">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="3a3c2-168">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-168">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3a3c2-169">너무 이동**SAML 서명 인증서** 섹션에서 다음 클릭 **다운로드** 열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-169">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="3a3c2-170">어떤 hello 응용 프로그램에 single sign-on 구성 필요한 경우에 따라 메타 데이터 XML hello 또는 인증서를 환영 hello 옵션 toodownload를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-170">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="3a3c2-171">Azure AD URL tooget hello 메타 데이터를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-171">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="3a3c2-172">hello 메타 데이터를 XML 파일로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-172">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-toohello-application"></a><span data-ttu-id="3a3c2-173">사용자가 toohello 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="3a3c2-173">Assign users toohello application</span></span>

<span data-ttu-id="3a3c2-174">tooassign 아래의 hello 단계를 직접 수행 하는 하나 이상의 사용자가 tooan 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="3a3c2-174">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="3a3c2-175">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="3a3c2-175">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3a3c2-176">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-176">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3a3c2-177">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-177">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3a3c2-178">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-178">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3a3c2-179">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-179">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="3a3c2-180">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="3a3c2-180">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="3a3c2-181">원하는 사용자 toofrom hello 목록 tooassign hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-181">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="3a3c2-182">Hello 응용 프로그램 로드 되 면 클릭 **사용자 및 그룹** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-182">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3a3c2-183">Hello 클릭 **추가** hello 위로 단추 **사용자 및 그룹** 목록 tooopen hello **할당 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-183">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="3a3c2-184">hello 클릭 **사용자 및 그룹** hello에서 선택기 **할당 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-184">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="3a3c2-185">Hello 입력 **전체 이름** 또는 **전자 메일 주소** hello에 할당 하려는 hello 사용자의 **이름 또는 전자 메일 주소로 검색을 통해** 검색 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-185">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="3a3c2-186">Hello 위로 마우스를 가져가고 **사용자** hello 목록 tooreveal에는 **확인란**합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-186">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="3a3c2-187">Hello 확인란 다음 toohello 사용자의 프로필 사진 또는 로고 tooadd 사용자 toohello 클릭 **선택한** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-187">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="3a3c2-188">**선택 사항:** 너무 원하는 경우**둘 이상의 사용자를 추가**, 다른 유형 **전체 이름** 또는 **전자 메일 주소** hello에 **이름으로 검색 전자 메일 주소 또는** 상자에서 검색 하 고이 사용자 toohello hello 확인란 tooadd 클릭 **선택한** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-188">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="3a3c2-189">사용자 선택을 완료 했으면 클릭 hello **선택** 단추 tooadd 해당 사용자 및 그룹 toobe toohello 목록이 toohello 응용 프로그램을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-189">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="3a3c2-190">**선택 사항:** hello 클릭 **역할 선택** hello에 선택 기가 **할당 추가** 블레이드 tooselect 역할 tooassign toohello 사용자가 선택한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-190">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="3a3c2-191">Hello 클릭 **할당** 단추 tooassign hello 응용 프로그램 toohello 사용자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-191">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="3a3c2-192">시간의 짧은 기간 이후에 hello 사용자가 선택한 이러한 응용 프로그램을 사용 하 여 hello hello 솔루션 설명 섹션에 설명 된 방법 수 toolaunch 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-192">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="3a3c2-193">Tooan 응용 프로그램 보낸 hello SAML 클레임 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="3a3c2-193">Customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="3a3c2-194">toolearn toocustomize hello SAML 특성 클레임 전송 tooyour 응용 프로그램 참조 [Azure Active Directory에서 매핑을 클레임](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-194">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a3c2-195">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3a3c2-195">Next steps</span></span>
[<span data-ttu-id="3a3c2-196">응용 프로그램 프록시 single sign on tooyour 앱을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a3c2-196">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
