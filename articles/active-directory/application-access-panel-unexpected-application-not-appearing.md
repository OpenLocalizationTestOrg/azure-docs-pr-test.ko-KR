---
title: "할당 된 aaaAn 응용 프로그램은 hello 액세스 패널에 표시 되지 않는 | Microsoft Docs"
description: "응용 프로그램은 hello 액세스 패널에에서 표시 되지 않는 한 문제 해결"
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
ms.reviwer: japere
ms.openlocfilehash: 089883f406267df4552c7fc991883f335ad49fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="an-assigned-application-is-not-appearing-on-hello-access-panel"></a><span data-ttu-id="333a8-103">할당된 된 응용 프로그램은 hello 액세스 패널에 표시 되지 않는</span><span class="sxs-lookup"><span data-stu-id="333a8-103">An assigned application is not appearing on hello access panel</span></span>

<span data-ttu-id="333a8-104">hello 액세스 패널은 작업으로는 사용할 수 있는 웹 기반 포털 또는 학교 계정을 Azure Active Directory (Azure AD) tooview 및 시작 클라우드 기반 응용 프로그램에서 해당 hello Azure AD 관리자가 부여 해 준에 대 한 액세스.</span><span class="sxs-lookup"><span data-stu-id="333a8-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="333a8-105">이러한 응용 프로그램 hello Azure AD 포털에서 hello 사용자를 대신 하 여 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="333a8-106">hello 응용 프로그램을 올바르게 구성 되어야 합니다. 및 할당 된 toohello 사용자 또는 그룹 hello 사용자가 hello 액세스 패널에에서 toosee hello 응용 프로그램의 구성원입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="333a8-107">사용자 표시 될 수는 앱의 hello 유형 hello 다음 범주에에서 속합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-107">hello type of apps a user may be seeing fall in hello following categories:</span></span>

-   <span data-ttu-id="333a8-108">Office 365 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="333a8-108">Office 365 Applications</span></span>

-   <span data-ttu-id="333a8-109">페더레이션 기반 SSO로 구성된 Microsoft 및 타사 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="333a8-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="333a8-110">암호 기반 SSO 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="333a8-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="333a8-111">기존 SSO 솔루션을 사용한 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="333a8-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="333a8-112">일반 toocheck를 먼저 문제</span><span class="sxs-lookup"><span data-stu-id="333a8-112">General issues toocheck first</span></span>

-   <span data-ttu-id="333a8-113">응용 프로그램 방금 tooa 사용자를 추가 하는 경우 다시 toosign 시작 및 종료 hello 사용자의 액세스 패널에 몇 분 toosee 후 hello 응용 프로그램에 추가 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="333a8-113">If an application was just added tooa user, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello application is added.</span></span>

-   <span data-ttu-id="333a8-114">사용자 또는 그룹 hello 사용자에서 라이선스가 제거 방금 되었으면는이 멤버는 변경 내용 toobe 수행에 대 한 hello 그룹의 hello 크기와 복잡성에 따라 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-114">If a license was just removed from a user or group hello user is a member of this may take a long time, depending on hello size and complexity of hello group for changes toobe made.</span></span> <span data-ttu-id="333a8-115">Hello 액세스 패널에 로그인 하기 전에 추가 시간을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-115">Allow for extra time before signing into hello Access Panel.</span></span>

## <a name="problems-related-tooapplication-configuration"></a><span data-ttu-id="333a8-116">문제 관련된 tooapplication 구성</span><span class="sxs-lookup"><span data-stu-id="333a8-116">Problems related tooapplication configuration</span></span>

<span data-ttu-id="333a8-117">응용 프로그램이 올바르게 구성되지 않아서 사용자의 액세스 패널에 표시되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-117">An application may not be appearing in a user’s Access Panel because it is not configured properly.</span></span> <span data-ttu-id="333a8-118">다음은 몇 가지 관련된 tooapplication 구성 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-118">Below are some ways you can troubleshoot issues related tooapplication configuration:</span></span>

-   [<span data-ttu-id="333a8-119">Single sign on Azure AD 갤러리 응용 프로그램에 대 한 tooconfigure 페더레이션 하는 방법</span><span class="sxs-lookup"><span data-stu-id="333a8-119">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application)

-   [<span data-ttu-id="333a8-120">Single sign on 갤러리가 아닌 응용 프로그램에 대 한 tooconfigure 페더레이션 하는 방법</span><span class="sxs-lookup"><span data-stu-id="333a8-120">How tooconfigure federated single sign-on for a non-gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="333a8-121">어떻게 tooconfigure 암호 single sign-on 응용 프로그램에 대 한 Azure AD 갤러리 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="333a8-121">How tooconfigure a password single sign-on application for an Azure AD gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="333a8-122">어떻게 tooconfigure 암호 single sign-on 응용 프로그램 갤러리가 아닌 응용 프로그램에 대 한</span><span class="sxs-lookup"><span data-stu-id="333a8-122">How tooconfigure a password single sign-on application for a non-gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

### <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="333a8-123">Single sign on Azure AD 갤러리 응용 프로그램에 대 한 tooconfigure 페더레이션 하는 방법</span><span class="sxs-lookup"><span data-stu-id="333a8-123">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="333a8-124">Enterprise Single Sign-on 기능을 사용 하도록 설정 하는 hello Azure AD 갤러리의 모든 응용 프로그램에는 단계별 자습서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-124">All applications in hello Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="333a8-125">Hello에 액세스할 수 있습니다 [방법에 대 한 자습서 목록 toointegrate SaaS 앱 Azure Active Directory와](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) 세부 단계별 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-125">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="333a8-126">tooconfigure hello Azure AD 갤러리에서 응용 프로그램 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-126">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="333a8-127">Hello Azure AD 갤러리에서 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="333a8-127">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="333a8-128">Azure ad (로그온 URL, 식별자, 회신 URL) hello 응용 프로그램의 메타 데이터 값을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-128">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="333a8-129">사용자의 Id를 선택 하 고 사용자 특성 전송 toobe toohello 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="333a8-129">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="333a8-130">Azure AD 메타데이터 및 인증서 검색</span><span class="sxs-lookup"><span data-stu-id="333a8-130">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="333a8-131">Hello 응용 프로그램 (로그온 URL, 발급자, 로그 아웃 URL 및 인증서)에 Azure AD 메타 데이터 값을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-131">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="333a8-132">Hello Azure AD 갤러리에서 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="333a8-132">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="333a8-133">아래의 hello 단계를 수행 하는 tooadd hello Azure AD 갤러리에서에서 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="333a8-133">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="333a8-134">열기 hello [Azure 포털](https://portal.azure.com) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="333a8-134">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="333a8-135">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-135">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="333a8-136">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-136">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="333a8-137">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-137">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="333a8-138">hello 클릭 **추가** hello hello 오른쪽 위 모서리에 있는 단추 **엔터프라이즈 응용 프로그램** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-138">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="333a8-139">Hello에 **이름을 입력** hello에서 텍스트 상자에 붙여넣습니다 **hello 갤러리에서 추가** 섹션, hello 응용 프로그램의 형식 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-139">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="333a8-140">Single sign on tooconfigure 원하는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-140">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="333a8-141">Hello 응용 프로그램을 추가 하기 전에 hello에서 이름을 변경할 수 **이름** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-141">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="333a8-142">클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-142">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="333a8-143">짧은 시간 후 수 toosee hello 응용 프로그램의 구성 블레이드에서 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-143">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="333a8-144">Single sign on hello Azure AD 갤러리에서 응용 프로그램에 대 한 구성</span><span class="sxs-lookup"><span data-stu-id="333a8-144">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="333a8-145">tooconfigure single sign on 응용 프로그램에 대 한 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-145">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="333a8-146">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="333a8-146">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="333a8-147">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-147">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="333a8-148">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-148">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="333a8-149">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-149">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="333a8-150">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-150">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="333a8-151">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="333a8-151">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="333a8-152">Tooconfigure single sign on 원하는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-152">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="333a8-153">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-153">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="333a8-154">선택 **SAML 기반 로그온** hello에서 **모드** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-154">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="333a8-155">필요한 hello 값을 입력 **도메인 및 Url입니다.**</span><span class="sxs-lookup"><span data-stu-id="333a8-155">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="333a8-156">Hello 응용 프로그램 공급 업체에서 이러한 값을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-156">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="333a8-157">SP에서 시작한 SSO와 tooconfigure hello 응용 프로그램 hello 로그인 URL에 필요한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-157">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="333a8-158">일부 응용 프로그램에 대 한 hello 식별자도 필요한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-158">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="333a8-159">IdP에서 시작한 SSO, hello 필수 값입니다. 회신 URL로 tooconfigure hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-159">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="333a8-160">일부 응용 프로그램에 대 한 hello 식별자도 필요한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-160">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="333a8-161">**선택 사항:** 클릭 **고급 URL 설정 표시** toosee hello 선택적 값입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-161">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="333a8-162">Hello에 **사용자 특성**, 선택 hello에 있는 사용자에 대 한 고유 식별자를 hello **사용자 식별자** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-162">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="333a8-163">**선택 사항:** 클릭 **보기 및 다른 모든 사용자 특성 편집** tooedit hello 사용자가 로그인 할 때 hello SAML 토큰에서 보낸 toobe toohello 응용 프로그램 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-163">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="333a8-164">tooadd 특성:</span><span class="sxs-lookup"><span data-stu-id="333a8-164">tooadd an attribute:</span></span>

   1. <span data-ttu-id="333a8-165">**특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-165">click **Add attribute**.</span></span> <span data-ttu-id="333a8-166">Hello 입력 **이름** 및 hello 선택 hello **값** hello 드롭다운에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-166">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="333a8-167">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-167">click **Save.**</span></span> <span data-ttu-id="333a8-168">Hello 테이블에 새 특성을 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-168">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="333a8-169">클릭 **구성 &lt;응용 프로그램 이름&gt;**  방법은 tooaccess 설명서 tooconfigure single sign on hello 응용 프로그램에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-169">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="333a8-170">또한 hello 메타 데이터 Url 및 hello 응용 프로그램과 함께 필요한 인증서 toosetup SSO에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-170">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="333a8-171">클릭 **저장** toosave hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-171">click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="333a8-172">Toohello 응용 프로그램 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-172">Assign users toohello application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="333a8-173">사용자의 Id를 선택 하 고 사용자 특성 전송 toobe toohello 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="333a8-173">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="333a8-174">tooselect hello 사용자 식별자 또는 사용자 특성 추가, 아래의 hello 단계를 수행:</span><span class="sxs-lookup"><span data-stu-id="333a8-174">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="333a8-175">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="333a8-175">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="333a8-176">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-176">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="333a8-177">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-177">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="333a8-178">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-178">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="333a8-179">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-179">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="333a8-180">Hello를 사용 하 여 원하는 여기 tooshow hello 응용 프로그램을 표시 되지 않으면 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="333a8-180">If you do not see hello application you want tooshow up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="333a8-181">Single sign on 구성한 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-181">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="333a8-182">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-182">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="333a8-183">Hello에서 **사용자 특성** 섹션에서 사용자 hello에 대 한 고유 식별자를 hello **사용자 식별자** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-183">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="333a8-184">hello 선택된 된 옵션 두어야 hello 응용 프로그램 tooauthenticate hello 사용자에서 toomatch hello 예상 값.</span><span class="sxs-lookup"><span data-stu-id="333a8-184">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="333a8-185">Hello NameID 특성 (사용자 식별자)에 대 한 azure AD 선택 hello 형식 선택한 hello 값에 따라 또는 hello SAML AuthRequest hello에 hello 응용 프로그램에서 요청한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-185">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="333a8-186">자세한 내용은 방문 hello 문서 [Single Sign On SAML 프로토콜](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) hello에서 NameIDPolicy 섹션.</span><span class="sxs-lookup"><span data-stu-id="333a8-186">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="333a8-187">tooadd 사용자 특성을 클릭 하 여 **보기 및 다른 모든 사용자 특성을 편집** tooedit hello 사용자가 로그인 할 때 hello SAML 토큰에서 보낸 toobe toohello 응용 프로그램 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-187">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="333a8-188">tooadd 특성:</span><span class="sxs-lookup"><span data-stu-id="333a8-188">tooadd an attribute:</span></span>

   1. <span data-ttu-id="333a8-189">**특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-189">click **Add attribute**.</span></span> <span data-ttu-id="333a8-190">Hello 입력 **이름** 및 hello 선택 hello **값** hello 드롭다운에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-190">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="333a8-191">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-191">click **Save.**</span></span> <span data-ttu-id="333a8-192">Hello hello 테이블에 새 특성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-192">You will see hello new attribute in hello table.</span></span>

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="333a8-193">Hello Azure AD 메타 데이터 또는 인증서를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-193">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="333a8-194">toodownload hello에 대 한 응용 프로그램 메타 데이터 또는 Azure AD에서 인증서를 다음 hello 단계를 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-194">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="333a8-195">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="333a8-195">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="333a8-196">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-196">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="333a8-197">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-197">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="333a8-198">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-198">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="333a8-199">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-199">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="333a8-200">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="333a8-200">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="333a8-201">Single sign on 구성한 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-201">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="333a8-202">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-202">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="333a8-203">너무 이동**SAML 서명 인증서** 섹션에서 다음 클릭 **다운로드** 열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-203">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="333a8-204">어떤 hello 응용 프로그램에 single sign-on 구성 필요한 경우에 따라 메타 데이터 XML hello 또는 인증서를 환영 hello 옵션 toodownload를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-204">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="333a8-205">Azure AD URL tooget hello 메타 데이터를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-205">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="333a8-206">hello 메타 데이터를 XML 파일로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-206">hello metadata can only be retrieved as a XML file.</span></span>

### <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="333a8-207">Single sign on 갤러리가 아닌 응용 프로그램에 대 한 tooconfigure 페더레이션 하는 방법</span><span class="sxs-lookup"><span data-stu-id="333a8-207">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="333a8-208">toohave Azure AD premium이 필요 tooconfigure 갤러리가 아닌 응용 프로그램 및 hello 응용 프로그램이 SAML 2.0을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-208">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="333a8-209">Azure AD 버전에 대한 자세한 내용은 [Azure AD 가격 책정](https://azure.microsoft.com/pricing/details/active-directory/)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-209">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="333a8-210">Azure ad (로그온 URL, 식별자, 회신 URL) hello 응용 프로그램의 메타 데이터 값을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-210">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="333a8-211">사용자의 Id를 선택 하 고 사용자 특성 전송 toobe toohello 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="333a8-211">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="333a8-212">Azure AD 메타데이터 및 인증서 검색</span><span class="sxs-lookup"><span data-stu-id="333a8-212">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="333a8-213">Hello 응용 프로그램 (로그온 URL, 발급자, 로그 아웃 URL 및 인증서)에 Azure AD 메타 데이터 값을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-213">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

#### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="333a8-214">Azure ad (로그온 URL, 식별자, 회신 URL) hello 응용 프로그램의 메타 데이터 값을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-214">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="333a8-215">tooconfigure single sign on hello Azure AD 갤러리에 없는 응용 프로그램에 대 한 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-215">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="333a8-216">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="333a8-216">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="333a8-217">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-217">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="333a8-218">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-218">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="333a8-219">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-219">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="333a8-220">hello 클릭 **추가** hello hello 오른쪽 위 모서리에 있는 단추 **엔터프라이즈 응용 프로그램** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-220">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="333a8-221">클릭 **비 갤러리 응용 프로그램** hello에 **위해 자신의 앱 추가** 섹션.</span><span class="sxs-lookup"><span data-stu-id="333a8-221">click **Non-gallery application** in hello **Add your own app** section.</span></span>

7.  <span data-ttu-id="333a8-222">Hello에 hello 응용 프로그램의 hello 이름을 입력 **이름** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-222">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="333a8-223">클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-223">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="333a8-224">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-224">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="333a8-225">선택 **SAML 기반 로그온** hello에 **모드** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-225">Select **SAML-based Sign-on** in hello **Mode** dropdown.</span></span>

11. <span data-ttu-id="333a8-226">필요한 hello 값을 입력 **도메인 및 Url입니다.**</span><span class="sxs-lookup"><span data-stu-id="333a8-226">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="333a8-227">Hello 응용 프로그램 공급 업체에서 이러한 값을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-227">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="333a8-228">IdP에서 시작한 SSO와 tooconfigure hello 응용 프로그램 회신 URL hello 및 hello 식별자를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-228">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

   2.  <span data-ttu-id="333a8-229">**선택 사항:** SP에서 시작한 SSO와 tooconfigure hello 응용 프로그램 hello 로그인 URL에 필요한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-229">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="333a8-230">Hello에 **사용자 특성**, 선택 hello에 있는 사용자에 대 한 고유 식별자를 hello **사용자 식별자** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-230">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="333a8-231">**선택 사항:** 클릭 **보기 및 다른 모든 사용자 특성 편집** tooedit hello 사용자가 로그인 할 때 hello SAML 토큰에서 보낸 toobe toohello 응용 프로그램 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-231">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="333a8-232">tooadd 특성:</span><span class="sxs-lookup"><span data-stu-id="333a8-232">tooadd an attribute:</span></span>

   1. <span data-ttu-id="333a8-233">**특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-233">click **Add attribute**.</span></span> <span data-ttu-id="333a8-234">Hello 입력 **이름** 및 hello 선택 hello **값** hello 드롭다운에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-234">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="333a8-235">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-235">Click **Save.**</span></span> <span data-ttu-id="333a8-236">Hello 테이블에 새 특성을 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-236">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="333a8-237">클릭 **구성 &lt;응용 프로그램 이름&gt;**  방법은 tooaccess 설명서 tooconfigure single sign on hello 응용 프로그램에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-237">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="333a8-238">또한 Azure AD Url 및 hello 응용 프로그램에 필요한 인증서에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-238">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="333a8-239">사용자의 Id를 선택 하 고 사용자 특성 전송 toobe toohello 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="333a8-239">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="333a8-240">tooselect hello 사용자 식별자 또는 사용자 특성 추가, 아래의 hello 단계를 수행:</span><span class="sxs-lookup"><span data-stu-id="333a8-240">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="333a8-241">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="333a8-241">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="333a8-242">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-242">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="333a8-243">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-243">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="333a8-244">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-244">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="333a8-245">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-245">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="333a8-246">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="333a8-246">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="333a8-247">Single sign on 구성한 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-247">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="333a8-248">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-248">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="333a8-249">Hello에서 **사용자 특성** 섹션에서 사용자 hello에 대 한 고유 식별자를 hello **사용자 식별자** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-249">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="333a8-250">hello 선택된 된 옵션 두어야 hello 응용 프로그램 tooauthenticate hello 사용자에서 toomatch hello 예상 값.</span><span class="sxs-lookup"><span data-stu-id="333a8-250">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="333a8-251">Hello NameID 특성 (사용자 식별자)에 대 한 azure AD 선택 hello 형식 선택한 hello 값에 따라 또는 hello SAML AuthRequest hello에 hello 응용 프로그램에서 요청한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-251">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="333a8-252">자세한 내용은 방문 hello 문서 [Single Sign On SAML 프로토콜](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) hello에서 NameIDPolicy 섹션.</span><span class="sxs-lookup"><span data-stu-id="333a8-252">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="333a8-253">tooadd 사용자 특성을 클릭 하 여 **보기 및 다른 모든 사용자 특성을 편집** tooedit hello 사용자가 로그인 할 때 hello SAML 토큰에서 보낸 toobe toohello 응용 프로그램 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-253">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="333a8-254">tooadd 특성:</span><span class="sxs-lookup"><span data-stu-id="333a8-254">tooadd an attribute:</span></span>

   1. <span data-ttu-id="333a8-255">**특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-255">click **Add attribute**.</span></span> <span data-ttu-id="333a8-256">Hello 입력 **이름** 및 hello 선택 hello **값** hello 드롭다운에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-256">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="333a8-257">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-257">Click **Save.**</span></span> <span data-ttu-id="333a8-258">Hello 테이블에 새 특성을 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-258">You see hello new attribute in hello table.</span></span>

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="333a8-259">Hello Azure AD 메타 데이터 또는 인증서를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-259">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="333a8-260">toodownload hello에 대 한 응용 프로그램 메타 데이터 또는 Azure AD에서 인증서를 다음 hello 단계를 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-260">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="333a8-261">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="333a8-261">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="333a8-262">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-262">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="333a8-263">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-263">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="333a8-264">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-264">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="333a8-265">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-265">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="333a8-266">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="333a8-266">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="333a8-267">Single sign on 구성한 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-267">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="333a8-268">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-268">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="333a8-269">너무 이동**SAML 서명 인증서** 섹션에서 다음 클릭 **다운로드** 열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-269">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="333a8-270">어떤 hello 응용 프로그램에 single sign-on 구성 필요한 경우에 따라 메타 데이터 XML hello 또는 인증서를 환영 hello 옵션 toodownload를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-270">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="333a8-271">Azure AD URL tooget hello 메타 데이터를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-271">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="333a8-272">hello 메타 데이터를 XML 파일로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-272">hello metadata can only be retrieved as a XML file.</span></span>

### <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="333a8-273">Azure AD 갤러리 응용 프로그램에 대 한 sign-on tooconfigure 암호 single 방법</span><span class="sxs-lookup"><span data-stu-id="333a8-273">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="333a8-274">tooconfigure hello Azure AD 갤러리에서 응용 프로그램 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-274">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="333a8-275">Hello Azure AD 갤러리에서 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="333a8-275">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="333a8-276">암호 single sign on에 대 한 hello 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="333a8-276">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="333a8-277">Hello Azure AD 갤러리에서 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="333a8-277">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="333a8-278">아래의 hello 단계를 수행 하는 tooadd hello Azure AD 갤러리에서에서 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="333a8-278">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="333a8-279">열기 hello [Azure 포털](https://portal.azure.com) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="333a8-279">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="333a8-280">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-280">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="333a8-281">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-281">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="333a8-282">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-282">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="333a8-283">hello 클릭 **추가** hello hello 오른쪽 위 모서리에 있는 단추 **엔터프라이즈 응용 프로그램** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-283">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="333a8-284">Hello에 **이름을 입력** hello에서 텍스트 상자에 붙여넣습니다 **hello 갤러리에서 추가** 섹션, hello 응용 프로그램의 형식 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-284">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="333a8-285">Single sign on tooconfigure 원하는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-285">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="333a8-286">Hello 응용 프로그램을 추가 하기 전에 hello에서 이름을 변경할 수 **이름** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-286">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="333a8-287">클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-287">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="333a8-288">짧은 시간 후 수 toosee hello 응용 프로그램의 구성 블레이드에서 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-288">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="333a8-289">암호 single sign on에 대 한 hello 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="333a8-289">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="333a8-290">tooconfigure single sign on 응용 프로그램에 대 한 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-290">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="333a8-291">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="333a8-291">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="333a8-292">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-292">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="333a8-293">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-293">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="333a8-294">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-294">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="333a8-295">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-295">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="333a8-296">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="333a8-296">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="333a8-297">Tooconfigure single sign on 원하는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-297">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="333a8-298">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-298">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="333a8-299">선택 hello 모드 **암호 기반 로그온 합니다.**</span><span class="sxs-lookup"><span data-stu-id="333a8-299">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="333a8-300">[Toohello 응용 프로그램 사용자를 할당](#how-to-assign-a-user-to-an-application-directly)합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-300">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="333a8-301">Hello 사용자의 hello 행을 선택 하 고를 클릭 하 여 hello 사용자 대신 자격 증명도 제공할 수 또한 **업데이트 자격 증명** hello 사용자를 대신해 서 hello 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-301">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="333a8-302">그렇지 않은 경우 사용자 수 증명된 tooenter hello 자격 증명 자체 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-302">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

### <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="333a8-303">Tooconfigure 암호 로그온 갤러리가 아닌 응용 프로그램에 대 한 단일 하는 방법</span><span class="sxs-lookup"><span data-stu-id="333a8-303">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="333a8-304">tooconfigure hello Azure AD 갤러리에서 응용 프로그램 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-304">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="333a8-305">비갤러리 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="333a8-305">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="333a8-306">암호 single sign on에 대 한 hello 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="333a8-306">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-a-non-gallery-application"></a><span data-ttu-id="333a8-307">비갤러리 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="333a8-307">Add a non-gallery application</span></span>

<span data-ttu-id="333a8-308">아래의 hello 단계를 수행 하는 tooadd hello Azure AD 갤러리에서에서 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="333a8-308">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="333a8-309">열기 hello [Azure 포털](https://portal.azure.com) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-309">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="333a8-310">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-310">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="333a8-311">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-311">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="333a8-312">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-312">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="333a8-313">hello 클릭 **추가** hello hello 오른쪽 위 모서리에 있는 단추 **엔터프라이즈 응용 프로그램** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-313">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="333a8-314">**비갤러리 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-314">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="333a8-315">Hello에 응용 프로그램의 hello 이름을 입력 **이름** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-315">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="333a8-316">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-316">Select **Add.**</span></span>

<span data-ttu-id="333a8-317">짧은 시간 후 수 toosee hello 응용 프로그램의 구성 블레이드에서 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-317">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="333a8-318">암호 single sign on에 대 한 hello 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="333a8-318">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="333a8-319">tooconfigure single sign on 응용 프로그램에 대 한 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-319">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="333a8-320">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="333a8-320">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="333a8-321">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-321">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="333a8-322">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-322">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="333a8-323">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-323">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="333a8-324">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-324">click **All Applications** tooview a list of all your applications.</span></span>

    1.  <span data-ttu-id="333a8-325">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="333a8-325">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="333a8-326">Tooconfigure single sign on 원하는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-326">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="333a8-327">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-327">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="333a8-328">선택 hello 모드 **암호 기반 로그온 합니다.**</span><span class="sxs-lookup"><span data-stu-id="333a8-328">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="333a8-329">Hello 입력 **로그온 URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-329">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="333a8-330">사용자가을 자신의 사용자 이름 및 암호 toosign 입력할 수 있는 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-330">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="333a8-331">Hello 로그인 필드 hello URL에 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-331">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="333a8-332">[Toohello 응용 프로그램 사용자를 할당](#how-to-assign-a-user-to-an-application-directly)합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-332">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

11. <span data-ttu-id="333a8-333">Hello 사용자의 hello 행을 선택 하 고를 클릭 하 여 hello 사용자 대신 자격 증명도 제공할 수 또한 **업데이트 자격 증명** hello 사용자를 대신해 서 hello 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-333">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="333a8-334">그렇지 않은 경우 사용자 수 증명된 tooenter hello 자격 증명 자체 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-334">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="problems-related-tooassigning-applications-toousers"></a><span data-ttu-id="333a8-335">문제 관련된 tooassigning 응용 프로그램 toousers</span><span class="sxs-lookup"><span data-stu-id="333a8-335">Problems related tooassigning applications toousers</span></span>

<span data-ttu-id="333a8-336">사용자 하지 표시 될 수는 응용 프로그램 액세스 패널에서 toohello 응용 프로그램 할당 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-336">A user may not be seeing an application on their Access Panel because they are not assigned toohello application.</span></span> <span data-ttu-id="333a8-337">다음은 몇 가지 방법으로 toocheck입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-337">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="333a8-338">사용자가 toohello 응용 프로그램을 할당 하는 경우 확인</span><span class="sxs-lookup"><span data-stu-id="333a8-338">Check if a user is assigned toohello application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="333a8-339">어떻게 tooassign 사용자 tooan 응용 프로그램을 직접</span><span class="sxs-lookup"><span data-stu-id="333a8-339">How tooassign a user tooan application directly</span></span>](#how-to-assign-a-user-to-an-application-directly)

-   [<span data-ttu-id="333a8-340">사용자가 tooa 라이선스가 할당 되었는지 확인 하 고 관련 toohello 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="333a8-340">Check if a user is assigned tooa license related toohello application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)

-   [<span data-ttu-id="333a8-341">어떻게 tooassign 라이선스 tooa 사용자</span><span class="sxs-lookup"><span data-stu-id="333a8-341">How tooassign a license tooa user</span></span>](#how-to-assign-a-user-a-license)

### <a name="check-if-a-user-is-assigned-toohello-application"></a><span data-ttu-id="333a8-342">사용자가 toohello 응용 프로그램을 할당 하는 경우 확인</span><span class="sxs-lookup"><span data-stu-id="333a8-342">Check if a user is assigned toohello application</span></span>

<span data-ttu-id="333a8-343">toocheck 사용자 toohello 응용 프로그램에 지정 되 면 hello 아래의 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-343">toocheck if a user is assigned toohello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="333a8-344">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="333a8-344">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="333a8-345">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-345">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="333a8-346">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-346">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="333a8-347">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-347">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="333a8-348">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-348">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="333a8-349">**검색** hello 응용 프로그램과의 hello 이름에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-349">**Search** for hello name of hello application in question.</span></span>

7.  <span data-ttu-id="333a8-350">**사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-350">click **Users and groups**.</span></span>

8.  <span data-ttu-id="333a8-351">이때 회원님의 사용자 toohello 응용 프로그램에 할당 된 경우 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-351">Check toosee if your user is assigned toohello application.</span></span>

   * <span data-ttu-id="333a8-352">hello 단계를 수행 하지 않은 경우 "어떻게 tooassign 사용자 tooan 응용 프로그램을 직접" toodo 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-352">If not follow hello steps in “How tooassign a user tooan application directly” toodo so.</span></span>

### <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="333a8-353">어떻게 tooassign 사용자 tooan 응용 프로그램을 직접</span><span class="sxs-lookup"><span data-stu-id="333a8-353">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="333a8-354">tooassign 아래의 hello 단계를 직접 수행 하는 하나 이상의 사용자가 tooan 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="333a8-354">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="333a8-355">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-355">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="333a8-356">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-356">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="333a8-357">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-357">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="333a8-358">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-358">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="333a8-359">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-359">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="333a8-360">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="333a8-360">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="333a8-361">원하는 사용자 toofrom hello 목록 tooassign hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-361">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="333a8-362">Hello 응용 프로그램 로드 되 면 클릭 **사용자 및 그룹** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-362">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="333a8-363">Hello 클릭 **추가** hello 위로 단추 **사용자 및 그룹** 목록 tooopen hello **할당 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-363">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="333a8-364">hello 클릭 **사용자 및 그룹** hello에서 선택기 **할당 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-364">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="333a8-365">Hello 입력 **전체 이름** 또는 **전자 메일 주소** hello에 할당 하려는 hello 사용자의 **이름 또는 전자 메일 주소로 검색을 통해** 검색 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-365">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="333a8-366">Hello 위로 마우스를 가져가고 **사용자** hello 목록 tooreveal에는 **확인란**합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-366">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="333a8-367">Hello 확인란 다음 toohello 사용자의 프로필 사진 또는 로고 tooadd 사용자 toohello 클릭 **선택한** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-367">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="333a8-368">**선택 사항:** 너무 원하는 경우**둘 이상의 사용자를 추가**, 다른 유형 **전체 이름** 또는 **전자 메일 주소** hello에 **이름으로 검색 전자 메일 주소 또는** 상자에서 검색 하 고이 사용자 toohello hello 확인란 tooadd 클릭 **선택한** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-368">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="333a8-369">사용자 선택을 완료 했으면 클릭 hello **선택** 단추 tooadd 해당 사용자 및 그룹 toobe toohello 목록이 toohello 응용 프로그램을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-369">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="333a8-370">**선택 사항:** hello 클릭 **역할 선택** hello에 선택 기가 **할당 추가** 블레이드 tooselect 역할 tooassign toohello 사용자가 선택한 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-370">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="333a8-371">Hello 클릭 **할당** 단추 tooassign hello 응용 프로그램 toohello 사용자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-371">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="333a8-372">짧은 기간 hello 사용자가 선택한 수 수 toolaunch에서 이러한 응용 프로그램 액세스 패널 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-372">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a><span data-ttu-id="333a8-373">사용자 라이선스 인지 확인 toohello 응용 프로그램 관련</span><span class="sxs-lookup"><span data-stu-id="333a8-373">Check if a user is under a license related toohello application</span></span>

<span data-ttu-id="333a8-374">toocheck 사용자의 라이선스를 다음 단계에 따라 hello 할당:</span><span class="sxs-lookup"><span data-stu-id="333a8-374">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="333a8-375">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="333a8-375">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="333a8-376">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-376">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="333a8-377">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-377">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="333a8-378">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-378">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="333a8-379">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-379">click **All users**.</span></span>

6.  <span data-ttu-id="333a8-380">**검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-380">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="333a8-381">클릭 **라이선스** toosee 현재 어떤 라이선스 hello 사용자에 게 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-381">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

  * <span data-ttu-id="333a8-382">Hello 사용자가 할당 된 tooan Office 라이선스 하는 경우 첫 번째 파티 Office 응용 프로그램 tooappear hello 사용자의 액세스 패널에 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-382">If hello user is assigned tooan Office license this enable First Party Office applications tooappear on hello user’s Access Panel.</span></span>

### <a name="how-tooassign-a-user-a-license"></a><span data-ttu-id="333a8-383">어떻게 tooassign 사용자 라이선스</span><span class="sxs-lookup"><span data-stu-id="333a8-383">How tooassign a user a license</span></span> 

<span data-ttu-id="333a8-384">아래의 hello 단계를 수행 하는 라이선스 tooa 사용자 tooassign:</span><span class="sxs-lookup"><span data-stu-id="333a8-384">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="333a8-385">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="333a8-385">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="333a8-386">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-386">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="333a8-387">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-387">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="333a8-388">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-388">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="333a8-389">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-389">click **All users**.</span></span>

6.  <span data-ttu-id="333a8-390">**검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-390">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="333a8-391">클릭 **라이선스** toosee 현재 어떤 라이선스 hello 사용자에 게 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-391">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="333a8-392">Hello 클릭 **할당** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-392">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="333a8-393">선택 **하나 이상의 제품** hello 사용 가능한 제품 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-393">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="333a8-394">**선택적** hello 클릭 **할당 옵션** 항목 toogranularly 제품을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-394">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="333a8-395">완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-395">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="333a8-396">Hello 클릭 **할당** tooassign 이러한 라이선스 toothis 사용자 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-396">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="problems-related-tooassigning-applications-toogroups"></a><span data-ttu-id="333a8-397">문제 관련된 tooassigning 응용 프로그램 toogroups</span><span class="sxs-lookup"><span data-stu-id="333a8-397">Problems related tooassigning applications toogroups</span></span>

<span data-ttu-id="333a8-398">사용자 표시 될 수는 응용 프로그램 액세스 패널에서 hello 응용 프로그램 할당 된 그룹의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-398">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned hello application.</span></span> <span data-ttu-id="333a8-399">다음은 몇 가지 방법으로 toocheck입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-399">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="333a8-400">사용자의 그룹 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="333a8-400">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="333a8-401">Tooassign 응용 프로그램 tooa 그룹화 방법을 직접</span><span class="sxs-lookup"><span data-stu-id="333a8-401">How tooassign an application tooa group directly</span></span>](#how-to-assign-an-application-to-a-group-directly)

-   [<span data-ttu-id="333a8-402">사용자 tooa 라이선스가 할당 된 그룹의 일부 인지 확인</span><span class="sxs-lookup"><span data-stu-id="333a8-402">Check if a user is part of group assigned tooa license</span></span>](#check-if-a-user-is-part-of-group-assigned-to-a-license)

-   [<span data-ttu-id="333a8-403">어떻게 tooassign 라이선스 tooa 그룹</span><span class="sxs-lookup"><span data-stu-id="333a8-403">How tooassign a license tooa group</span></span>](#how-to-assign-a-license-to-a-group)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="333a8-404">사용자의 그룹 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="333a8-404">Check a user’s group memberships</span></span>

<span data-ttu-id="333a8-405">toocheck 그룹의 구성원, 다음 단계에 따라 hello:</span><span class="sxs-lookup"><span data-stu-id="333a8-405">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="333a8-406">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="333a8-406">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="333a8-407">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-407">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="333a8-408">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-408">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="333a8-409">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-409">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="333a8-410">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-410">click **All users**.</span></span>

6.  <span data-ttu-id="333a8-411">**검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-411">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="333a8-412">**그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-412">click **Groups**.</span></span>

8.  <span data-ttu-id="333a8-413">이때 회원님의 사용자는 할당 된 그룹 toohello 응용 프로그램의 일부인 경우 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-413">Check toosee if your user is part of a Group assigned toohello application.</span></span>

  * <span data-ttu-id="333a8-414">Hello 그룹에서 사용자가 tooremove hello **hello 행 클릭** hello 그룹 및 삭제를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-414">If you want tooremove hello user from hello group, **click hello row** of hello group and select delete.</span></span>

### <a name="how-tooassign-an-application-tooa-group-directly"></a><span data-ttu-id="333a8-415">Tooassign 응용 프로그램 tooa 그룹화 방법을 직접</span><span class="sxs-lookup"><span data-stu-id="333a8-415">How tooassign an application tooa group directly</span></span>

<span data-ttu-id="333a8-416">하나 이상의 tooassign 그룹 tooan 응용 프로그램을 직접 아래 hello 단계 수행:</span><span class="sxs-lookup"><span data-stu-id="333a8-416">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="333a8-417">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-417">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="333a8-418">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-418">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="333a8-419">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-419">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="333a8-420">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-420">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="333a8-421">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-421">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="333a8-422">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="333a8-422">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="333a8-423">원하는 사용자 toofrom hello 목록 tooassign hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-423">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="333a8-424">Hello 응용 프로그램 로드 되 면 클릭 **사용자 및 그룹** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-424">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="333a8-425">Hello 클릭 **추가** hello 위로 단추 **사용자 및 그룹** 목록 tooopen hello **할당 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-425">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="333a8-426">hello 클릭 **사용자 및 그룹** hello에서 선택기 **할당 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-426">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="333a8-427">Hello 입력 **전체 그룹 이름** hello에 할당 하려는 hello 그룹의 **이름 또는 전자 메일 주소로 검색을 통해** 검색 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-427">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="333a8-428">Hello 위로 마우스를 가져가고 **그룹** hello 목록 tooreveal에는 **확인란**합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-428">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="333a8-429">Hello 확인란 다음 toohello 그룹의 프로필 사진 또는 로고 tooadd 사용자 toohello 클릭 **선택한** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-429">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="333a8-430">**선택 사항:** 너무 원하는 경우**둘 이상의 그룹을 추가**, 다른 유형 **전체 그룹 이름** hello에 **이름 또는 전자 메일 주소로 검색을 통해** 검색 상자 이 그룹 toohello hello 확인란 tooadd 클릭 **선택한** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-430">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="333a8-431">그룹을 선택 하면 완료 했으면 클릭 hello **선택** 단추 tooadd 해당 사용자 및 그룹 toobe toohello 목록이 toohello 응용 프로그램을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-431">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="333a8-432">**선택 사항:** hello 클릭 **역할 선택** hello에 선택 기가 **할당 추가** 블레이드 tooselect 역할 tooassign toohello 그룹 선택 했습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-432">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="333a8-433">Hello 클릭 **할당** 단추 tooassign hello 응용 프로그램 toohello 선택 된 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-433">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="333a8-434">짧은 기간 hello 사용자가 선택한 수 수 toolaunch에서 이러한 응용 프로그램 액세스 패널 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-434">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

### <a name="check-if-a-user-is-part-of-group-assigned-tooa-license"></a><span data-ttu-id="333a8-435">사용자 tooa 라이선스가 할당 된 그룹의 일부 인지 확인</span><span class="sxs-lookup"><span data-stu-id="333a8-435">Check if a user is part of group assigned tooa license</span></span>

1.  <span data-ttu-id="333a8-436">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="333a8-436">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="333a8-437">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-437">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="333a8-438">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-438">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="333a8-439">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-439">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="333a8-440">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-440">click **All users**.</span></span>

6.  <span data-ttu-id="333a8-441">**검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-441">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="333a8-442">**그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-442">click **Groups**.</span></span>

8.  <span data-ttu-id="333a8-443">특정 그룹의 hello 행을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-443">click hello row of a specific group.</span></span>

9.  <span data-ttu-id="333a8-444">클릭 **라이선스** toosee 라이선스 hello 그룹 tooit에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-444">click **Licenses** toosee which licenses hello group has assigned tooit.</span></span>

   * <span data-ttu-id="333a8-445">Hello 그룹이 할당 된 tooan Office 라이선스 이면이 hello 사용자의 액세스 패널에 첫 번째 파티 Office 응용 프로그램 tooappear 특정로 설정 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-445">If hello group is assigned tooan Office license this may enable certain First Party Office applications tooappear on hello user’s Access Panel.</span></span>

### <a name="how-tooassign-a-license-tooa-group"></a><span data-ttu-id="333a8-446">어떻게 tooassign 라이선스 tooa 그룹</span><span class="sxs-lookup"><span data-stu-id="333a8-446">How tooassign a license tooa group</span></span>

<span data-ttu-id="333a8-447">아래의 hello 단계를 수행 하는 라이선스 tooa 그룹을 tooassign:</span><span class="sxs-lookup"><span data-stu-id="333a8-447">tooassign a license tooa group, follow hello steps below:</span></span>

1.  <span data-ttu-id="333a8-448">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="333a8-448">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="333a8-449">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-449">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="333a8-450">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-450">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="333a8-451">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-451">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="333a8-452">**모든 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-452">click **All groups**.</span></span>

6.  <span data-ttu-id="333a8-453">**검색** 에 관심이 있는 hello 그룹에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-453">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="333a8-454">클릭 **라이선스** toosee 현재 hello 라이선스 그룹에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-454">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="333a8-455">Hello 클릭 **할당** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-455">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="333a8-456">선택 **하나 이상의 제품** hello 사용 가능한 제품 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-456">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="333a8-457">**선택적** hello 클릭 **할당 옵션** 항목 toogranularly 제품을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-457">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="333a8-458">완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-458">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="333a8-459">Hello 클릭 **할당** tooassign 이러한 라이선스 toothis 그룹 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-459">Click hello **Assign** button tooassign these licenses toothis group.</span></span> <span data-ttu-id="333a8-460">Hello 그룹의 hello 크기와 복잡성에 따라 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-460">This may take a long time, depending on hello size and complexity of hello group.</span></span>

>[!NOTE]
><span data-ttu-id="333a8-461">toodo이 더 빨리 고려 임시로 라이선스 toohello 사용자를 직접 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-461">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> 
>
>

## <a name="next-steps"></a><span data-ttu-id="333a8-462">다음 단계</span><span class="sxs-lookup"><span data-stu-id="333a8-462">Next steps</span></span>
[<span data-ttu-id="333a8-463">새 사용자 tooAzure Active Directory를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="333a8-463">Add new users tooAzure Active Directory</span></span>](active-directory-users-create-azure-portal.md)

