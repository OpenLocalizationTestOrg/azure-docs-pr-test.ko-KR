---
title: "single sign on Azure AD 갤러리 응용 프로그램에 대 한 페더레이션 aaaHow tooconfigure | Microsoft Docs"
description: "Single sign on는 기존 Azure AD 갤러리 응용 프로그램 및 사용 하 여 자습서 tooget 신속 하 게 진행에 대 한 tooconfigure 페더레이션 하는 방법"
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
ms.openlocfilehash: a93de021fddd253e4fe663c221b822d12625fd54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="b198e-103">Single sign on Azure AD 갤러리 응용 프로그램에 대 한 tooconfigure 페더레이션 하는 방법</span><span class="sxs-lookup"><span data-stu-id="b198e-103">How tooconfigure federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="b198e-104">Enterprise single sign-on 기능은 사용 하도록 설정 하는 Azure AD hello 갤러리의 모든 응용 프로그램에는 단계별 자습서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-104">All applications in hello Azure AD gallery enabled with Enterprise single sign-on capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="b198e-105">Hello에 액세스할 수 있습니다 [방법에 대 한 자습서 목록 toointegrate SaaS 앱 Azure Active Directory와](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) 자세한 단계별 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-105">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for detailed step-by-step guidance.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="b198e-106">필요한 단계 개요</span><span class="sxs-lookup"><span data-stu-id="b198e-106">Overview of steps required</span></span>
<span data-ttu-id="b198e-107">tooconfigure hello Azure AD 갤러리에서 응용 프로그램 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-107">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="b198e-108">Hello Azure AD 갤러리에서 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="b198e-108">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="b198e-109">Azure ad (로그온 URL, 식별자, 회신 URL) hello 응용 프로그램의 메타 데이터 값을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-109">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="b198e-110">사용자의 Id를 선택 하 고 사용자 특성 전송 toobe toohello 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="b198e-110">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="b198e-111">Azure AD 메타데이터 및 인증서 검색</span><span class="sxs-lookup"><span data-stu-id="b198e-111">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="b198e-112">Hello 응용 프로그램 (로그온 URL, 발급자, 로그 아웃 URL 및 인증서)에 Azure AD 메타 데이터 값을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-112">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="b198e-113">사용자가 toohello 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="b198e-113">Assign users toohello application</span></span>](#assign-users-to-the-application)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="b198e-114">Hello Azure AD 갤러리에서 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="b198e-114">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="b198e-115">아래의 hello 단계를 수행 하는 tooadd hello Azure AD 갤러리에서에서 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="b198e-115">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="b198e-116">열기 hello [Azure 포털](https://portal.azure.com) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="b198e-116">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="b198e-117">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b198e-118">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b198e-119">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b198e-120">hello 클릭 **추가** hello hello 오른쪽 위 모서리에 있는 단추 **엔터프라이즈 응용 프로그램** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-120">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="b198e-121">Hello에 **이름을 입력** hello에서 텍스트 상자에 붙여넣습니다 **hello 갤러리에서 추가** 섹션, hello 응용 프로그램의 형식 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-121">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="b198e-122">Single sign on tooconfigure 원하는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-122">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="b198e-123">Hello 응용 프로그램을 추가 하기 전에 hello에서 이름을 변경할 수 **이름** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-123">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="b198e-124">클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-124">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="b198e-125">시간의 짧은 기간 이후에 수 toosee hello 응용 프로그램의 구성 블레이드에서 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-125">After a short period of time, you be able toosee hello application’s configuration blade.</span></span>

## <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="b198e-126">Single sign on hello Azure AD 갤러리에서 응용 프로그램에 대 한 구성</span><span class="sxs-lookup"><span data-stu-id="b198e-126">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="b198e-127">tooconfigure single sign on 응용 프로그램에 대 한 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-127">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="b198e-128">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-128">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="b198e-129">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-129">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b198e-130">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-130">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b198e-131">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-131">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b198e-132">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-132">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="b198e-133">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="b198e-133">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b198e-134">Tooconfigure single sign on 원하는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-134">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="b198e-135">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-135">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b198e-136">선택 **SAML 기반 로그온** hello에서 **모드** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-136">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="b198e-137">필요한 hello 값을 입력 **도메인 및 Url입니다.**</span><span class="sxs-lookup"><span data-stu-id="b198e-137">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="b198e-138">Hello 응용 프로그램 공급 업체에서 이러한 값을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-138">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="b198e-139">SP에서 시작한 SSO와 tooconfigure hello 응용 프로그램 hello 로그인 URL에 필요한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-139">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="b198e-140">일부 응용 프로그램에 대 한 hello 식별자도 필요한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-140">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="b198e-141">IdP에서 시작한 SSO, hello 필수 값입니다. 회신 URL로 tooconfigure hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-141">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="b198e-142">일부 응용 프로그램에 대 한 hello 식별자도 필요한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-142">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="b198e-143">**선택 사항:** 클릭 **고급 URL 설정 표시** toosee hello 선택적 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-143">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="b198e-144">Hello에 **사용자 특성**, 선택 hello에 있는 사용자에 대 한 고유 식별자를 hello **사용자 식별자** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-144">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="b198e-145">**선택 사항:** 클릭 **보기 및 다른 모든 사용자 특성 편집** tooedit hello 사용자가 로그인 할 때 hello SAML 토큰에서 보낸 toobe toohello 응용 프로그램 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-145">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

  <span data-ttu-id="b198e-146">tooadd 특성:</span><span class="sxs-lookup"><span data-stu-id="b198e-146">tooadd an attribute:</span></span>
   
   1. <span data-ttu-id="b198e-147">**특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-147">click **Add attribute**.</span></span> <span data-ttu-id="b198e-148">Hello 입력 **이름** 및 hello 선택 hello **값** hello 드롭다운에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-148">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   1. <span data-ttu-id="b198e-149">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-149">Click **Save.**</span></span> <span data-ttu-id="b198e-150">Hello 테이블에 새 특성을 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-150">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="b198e-151">클릭 **구성 &lt;응용 프로그램 이름&gt;**  방법은 tooaccess 설명서 tooconfigure single sign on hello 응용 프로그램에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-151">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="b198e-152">또한 hello 메타 데이터 Url 및 hello 응용 프로그램과 함께 필요한 인증서 toosetup SSO에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-152">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="b198e-153">클릭 **저장** toosave hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-153">Click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="b198e-154">Toohello 응용 프로그램 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-154">Assign users toohello application.</span></span>

## <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="b198e-155">사용자의 Id를 선택 하 고 사용자 특성 전송 toobe toohello 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="b198e-155">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="b198e-156">tooselect hello 사용자 식별자 또는 사용자 특성 추가, 아래의 hello 단계를 수행:</span><span class="sxs-lookup"><span data-stu-id="b198e-156">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="b198e-157">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="b198e-157">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b198e-158">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b198e-159">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b198e-160">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b198e-161">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-161">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="b198e-162">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="b198e-162">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b198e-163">Single sign on 구성한 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-163">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="b198e-164">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-164">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b198e-165">Hello에서 **사용자 특성** 섹션에서 사용자 hello에 대 한 고유 식별자를 hello **사용자 식별자** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-165">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="b198e-166">hello 선택된 된 옵션 두어야 hello 응용 프로그램 tooauthenticate hello 사용자에서 toomatch hello 예상 값.</span><span class="sxs-lookup"><span data-stu-id="b198e-166">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

  >[!NOTE] 
  ><span data-ttu-id="b198e-167">Hello NameID 특성 (사용자 식별자)에 대 한 azure AD 선택 hello 형식 선택한 hello 값에 따라 또는 hello SAML AuthRequest hello에 hello 응용 프로그램에서 요청한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-167">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="b198e-168">자세한 내용은 방문 hello 문서 [Single Sign On SAML 프로토콜](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) hello에서 NameIDPolicy 섹션.</span><span class="sxs-lookup"><span data-stu-id="b198e-168">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
  >
  >

9.  <span data-ttu-id="b198e-169">tooadd 사용자 특성을 클릭 하 여 **보기 및 다른 모든 사용자 특성을 편집** tooedit hello 사용자가 로그인 할 때 hello SAML 토큰에서 보낸 toobe toohello 응용 프로그램 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-169">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="b198e-170">tooadd 특성:</span><span class="sxs-lookup"><span data-stu-id="b198e-170">tooadd an attribute:</span></span>
  
   1. <span data-ttu-id="b198e-171">**특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-171">click **Add attribute**.</span></span> <span data-ttu-id="b198e-172">Hello 입력 **이름** 및 hello 선택 hello **값** hello 드롭다운에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-172">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="b198e-173">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-173">Click **Save**.</span></span> <span data-ttu-id="b198e-174">Hello 테이블에 새 특성을 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-174">You see hello new attribute in hello table.</span></span>

## <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="b198e-175">Hello Azure AD 메타 데이터 또는 인증서를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-175">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="b198e-176">toodownload hello에 대 한 응용 프로그램 메타 데이터 또는 Azure AD에서 인증서를 다음 hello 단계를 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-176">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="b198e-177">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="b198e-177">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b198e-178">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-178">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b198e-179">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-179">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b198e-180">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-180">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b198e-181">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-181">click **All Applications** tooview a list of all your applications.</span></span>

  *  <span data-ttu-id="b198e-182">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-182">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications**.</span></span>

6.  <span data-ttu-id="b198e-183">Single sign on 구성한 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-183">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="b198e-184">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-184">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b198e-185">너무 이동**SAML 서명 인증서** 섹션에서 다음 클릭 **다운로드** 열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-185">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="b198e-186">어떤 hello 응용 프로그램에 single sign-on 구성 필요한 경우에 따라 메타 데이터 XML hello 또는 인증서를 환영 hello 옵션 toodownload를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-186">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="b198e-187">Azure AD URL tooget hello 메타 데이터를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-187">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="b198e-188">hello 메타 데이터를 XML 파일로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-188">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-toohello-application"></a><span data-ttu-id="b198e-189">사용자가 toohello 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="b198e-189">Assign users toohello application</span></span>

<span data-ttu-id="b198e-190">tooassign 아래의 hello 단계를 직접 수행 하는 하나 이상의 사용자가 tooan 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="b198e-190">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="b198e-191">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="b198e-191">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b198e-192">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-192">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b198e-193">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-193">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b198e-194">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-194">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b198e-195">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-195">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="b198e-196">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="b198e-196">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b198e-197">원하는 사용자 toofrom hello 목록 tooassign hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-197">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="b198e-198">Hello 응용 프로그램 로드 되 면 클릭 **사용자 및 그룹** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-198">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b198e-199">Hello 클릭 **추가** hello 위로 단추 **사용자 및 그룹** 목록 tooopen hello **할당 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-199">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="b198e-200">hello 클릭 **사용자 및 그룹** hello에서 선택기 **할당 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-200">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="b198e-201">Hello 입력 **전체 이름** 또는 **전자 메일 주소** hello에 할당 하려는 hello 사용자의 **이름 또는 전자 메일 주소로 검색을 통해** 검색 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-201">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="b198e-202">Hello 위로 마우스를 가져가고 **사용자** hello 목록 tooreveal에는 **확인란**합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-202">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="b198e-203">Hello 확인란 다음 toohello 사용자의 프로필 사진 또는 로고 tooadd 사용자 toohello 클릭 **선택한** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-203">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="b198e-204">**선택 사항:** 너무 원하는 경우**둘 이상의 사용자를 추가**, 다른 유형 **전체 이름** 또는 **전자 메일 주소** hello에 **이름으로 검색 전자 메일 주소 또는** 상자에서 검색 하 고이 사용자 toohello hello 확인란 tooadd 클릭 **선택한** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-204">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="b198e-205">사용자 선택을 완료 했으면 클릭 hello **선택** 단추 tooadd 해당 사용자 및 그룹 toobe toohello 목록이 toohello 응용 프로그램을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-205">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="b198e-206">**선택 사항:** hello 클릭 **역할 선택** hello에 선택 기가 **할당 추가** 블레이드 tooselect 역할 tooassign toohello 사용자가 선택한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-206">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="b198e-207">Hello 클릭 **할당** 단추 tooassign hello 응용 프로그램 toohello 사용자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-207">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="b198e-208">시간의 짧은 기간 이후에 hello 사용자가 선택한 이러한 응용 프로그램을 사용 하 여 hello hello 솔루션 설명 섹션에 설명 된 방법 수 toolaunch 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-208">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="b198e-209">Tooan 응용 프로그램 보낸 hello SAML 클레임 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="b198e-209">Customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="b198e-210">toolearn toocustomize hello SAML 특성 클레임 전송 tooyour 응용 프로그램 참조 [Azure Active Directory에서 매핑을 클레임](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-210">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b198e-211">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b198e-211">Next steps</span></span>
[<span data-ttu-id="b198e-212">응용 프로그램 프록시 single sign on tooyour 앱을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b198e-212">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)



