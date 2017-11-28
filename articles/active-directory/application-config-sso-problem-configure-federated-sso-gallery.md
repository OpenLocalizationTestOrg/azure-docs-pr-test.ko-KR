---
title: "페더레이션된 single sign-on 구성 Azure AD 갤러리 응용 프로그램에 대 한 aaaProblem | Microsoft Docs"
description: "단일 페더레이션 구성할 때 발생할 수 있는 hello 일반적인 문제 중 일부를 해결 hello Azure AD 응용 프로그램 갤러리에에서 나와 있는 응용 프로그램에 대 한 SAML을 사용 하 여 sign-on"
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
ms.openlocfilehash: 2ae1e511bd49b19159e1ab83cf79a7db5403b9a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="064e1-103">Azure AD 갤러리 응용 프로그램에 대해 페더레이션된 Single Sign-On을 구성할 때 발생하는 문제</span><span class="sxs-lookup"><span data-stu-id="064e1-103">Problem configuring federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="064e1-104">응용 프로그램을 구성할 때 문제가 발생 할 경우.</span><span class="sxs-lookup"><span data-stu-id="064e1-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="064e1-105">Hello 응용 프로그램에 대 한 hello 자습서의 모든 hello 단계를 따랐는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="064e1-105">Verify you have followed all hello steps in hello tutorial for hello application.</span></span> <span data-ttu-id="064e1-106">Hello 응용 프로그램의 구성에서 어떻게 tooconfigure hello 응용 프로그램에 대 한 인라인 문서가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-106">In hello application’s configuration, you have inline documentation on how tooconfigure hello application.</span></span> <span data-ttu-id="064e1-107">또한 hello에 액세스할 수 있습니다 [방법에 대 한 자습서 목록 toointegrate SaaS 앱 Azure Active Directory와](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) 세부 단계별 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-107">Also, you can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

## <a name="cant-add-another-instance-of-hello-application"></a><span data-ttu-id="064e1-108">Hello 응용 프로그램의 다른 인스턴스를 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-108">Can’t add another instance of hello application</span></span>

<span data-ttu-id="064e1-109">응용 프로그램의 두 번째 인스턴스 tooadd 필요한 toobe 수 있습니다:</span><span class="sxs-lookup"><span data-stu-id="064e1-109">tooadd a second instance of an application, you need toobe able to:</span></span>

-   <span data-ttu-id="064e1-110">Hello 두 번째 인스턴스에 대 한 고유 식별자를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-110">Configure a unique identifier for hello second instance.</span></span> <span data-ttu-id="064e1-111">동일한 식별자 사용에 대 한 hello 첫 번째 인스턴스 수 tooconfigure hello 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-111">You won’t be able tooconfigure hello same identifier used for hello first instance.</span></span>

-   <span data-ttu-id="064e1-112">첫 번째 인스턴스 hello에 대 한 사용 되는 hello와 다른 인증서를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-112">Configure a different certificate than hello one used for hello first instance.</span></span>

<span data-ttu-id="064e1-113">경우 hello 응용 프로그램 hello 위의 중 하나를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-113">If hello application doesn’t support any of hello above.</span></span> <span data-ttu-id="064e1-114">그런 다음 두 번째 인스턴스 수 tooconfigure 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-114">Then, you won’t be able tooconfigure a second instance.</span></span>

## <a name="cant-add-hello-identifier-or-hello-reply-url"></a><span data-ttu-id="064e1-115">Hello 식별자를 추가 하거나 회신 URL hello 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-115">Can’t add hello Identifier or hello Reply URL</span></span>

<span data-ttu-id="064e1-116">하지 수 tooconfigure hello 식별자 이거나 hello 회신 URL을 hello 식별자를 확인 하 고 회신 URL 값이 hello 응용 프로그램에 대해 미리 구성 하는 hello 패턴 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-116">If you’re not able tooconfigure hello Identifier or hello Reply URL, confirm hello Identifier and Reply URL values match hello patterns pre-configured for hello application.</span></span>

<span data-ttu-id="064e1-117">tooknow hello 패턴 hello 응용 프로그램에 대해 미리 구성:</span><span class="sxs-lookup"><span data-stu-id="064e1-117">tooknow hello patterns pre-configured for hello application:</span></span>

1.  <span data-ttu-id="064e1-118">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자** Toostep 7 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.** Go toostep 7.</span></span> <span data-ttu-id="064e1-119">이미 있다면 hello 응용 프로그램의 구성 블레이드에서 Azure AD에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-119">If you are already in hello application configuration blade on Azure AD.</span></span>

2.  <span data-ttu-id="064e1-120">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-120">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="064e1-121">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-121">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="064e1-122">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-122">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="064e1-123">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-123">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="064e1-124">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="064e1-124">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="064e1-125">Tooconfigure single sign on 원하는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-125">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="064e1-126">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-126">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="064e1-127">선택 **SAML 기반 로그온** hello에서 **모드** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-127">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="064e1-128">Toohello 이동 **식별자** 또는 **회신 URL** hello 아래 텍스트 상자 **도메인 및 Url 섹션입니다.**</span><span class="sxs-lookup"><span data-stu-id="064e1-128">Go toohello **Identifier** or **Reply URL** textbox, under hello **Domain and URLs section.**</span></span>

10. <span data-ttu-id="064e1-129">Hello 응용 프로그램에 tooknow 지원 hello 패턴은 다음 세 가지 방법:</span><span class="sxs-lookup"><span data-stu-id="064e1-129">There are three ways tooknow hello supported patterns for hello application:</span></span>

   * <span data-ttu-id="064e1-130">Hello 텍스트 자리 표시자로 hello 지원 케이스 참조 *예제:* <https://contoso.com>합니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-130">In hello textbox, you see hello supported pattern(s) as a placeholder *Example:* <https://contoso.com>.</span></span>

   * <span data-ttu-id="064e1-131">hello 패턴이 지원 되지 않는 hello 텍스트 상자의 tooenter hello 값 려 할 때 빨간색 느낌표가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-131">if hello pattern is not supported, you see a red exclamation mark when you try tooenter hello value in hello textbox.</span></span> <span data-ttu-id="064e1-132">Hello 빨간색 느낌표가 표시 위로 마우스를 가져가면 지원 hello 패턴을 파악 합니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-132">If you hover your mouse over hello red exclamation mark, you see hello supported patterns.</span></span>

   * <span data-ttu-id="064e1-133">Hello 응용 프로그램에 대 한 hello 자습서에서는 지원 되는 hello 패턴에 대 한 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-133">In hello tutorial for hello application, you can also get information about hello supported patterns.</span></span> <span data-ttu-id="064e1-134">Hello에서 **Azure AD single sign-on 구성** 섹션.</span><span class="sxs-lookup"><span data-stu-id="064e1-134">Under hello **Configure Azure AD single sign-on** section.</span></span> <span data-ttu-id="064e1-135">Hello 아래에 구성 된 hello 값에 대 한 이동 toohello 단계 **도메인 및 Url** 섹션.</span><span class="sxs-lookup"><span data-stu-id="064e1-135">Go toohello step for configured hello values under hello **Domain and URLs** section.</span></span>

<span data-ttu-id="064e1-136">경우 hello 값은 Azure AD에 미리 구성 된 hello 패턴과 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-136">If hello values don’t match with hello patterns pre-configured on Azure AD.</span></span> <span data-ttu-id="064e1-137">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-137">You can:</span></span>

-   <span data-ttu-id="064e1-138">Azure AD에 미리 구성 된 hello 패턴과 일치 하는 hello 응용 프로그램 공급 업체 tooget 값 사용</span><span class="sxs-lookup"><span data-stu-id="064e1-138">Work with hello application vendor tooget values that match hello pattern pre-configured on Azure AD</span></span>

-   <span data-ttu-id="064e1-139">Azure AD 팀에 문의할 수 있습니다 또는 < aadapprequest@microsoft.com > hello 응용 프로그램에 대 한 지원 hello 패턴의 hello 자습서 toorequest hello 업데이트에 의견을 남겨 또는</span><span class="sxs-lookup"><span data-stu-id="064e1-139">Or, you can contact Azure AD team at <aadapprequest@microsoft.com> or leave a comment in hello tutorial toorequest hello update of hello supported patterns for hello application</span></span>

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a><span data-ttu-id="064e1-140">Hello EntityID (사용자 식별자) 형식을 설정 하는 위치</span><span class="sxs-lookup"><span data-stu-id="064e1-140">Where do I set hello EntityID (User Identifier) format</span></span>

<span data-ttu-id="064e1-141">Azure AD는 hello에 대 한 응답 toohello 응용 프로그램 사용자 인증 후 보냅니다 수 tooselect hello EntityID (사용자 식별자) 형식 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-141">You won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="064e1-142">Hello NameID 특성 (사용자 식별자)에 대 한 azure AD 선택 hello 형식 선택한 hello 값에 따라 또는 hello SAML AuthRequest hello에 hello 응용 프로그램에서 요청한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-142">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="064e1-143">자세한 내용은 방문 hello 문서 [Single Sign On SAML 프로토콜](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) hello 섹션 NameIDPolicy,</span><span class="sxs-lookup"><span data-stu-id="064e1-143">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy,</span></span>

## <a name="cant-find-hello-azure-ad-metadata-toocomplete-hello-configuration-with-hello-application"></a><span data-ttu-id="064e1-144">Hello 응용 프로그램과 hello Azure AD 메타 데이터 toocomplete hello 구성을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-144">Can’t find hello Azure AD metadata toocomplete hello configuration with hello application</span></span>

<span data-ttu-id="064e1-145">toodownload hello에 대 한 응용 프로그램 메타 데이터 또는 Azure AD에서 인증서를 다음 hello 단계를 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-145">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="064e1-146">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="064e1-146">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="064e1-147">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-147">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="064e1-148">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-148">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="064e1-149">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-149">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="064e1-150">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-150">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="064e1-151">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="064e1-151">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="064e1-152">Single sign on 구성한 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-152">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="064e1-153">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-153">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="064e1-154">너무 이동**SAML 서명 인증서** 섹션에서 다음 클릭 **다운로드** 열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-154">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="064e1-155">어떤 hello 응용 프로그램에 single sign-on 구성 필요한 경우에 따라 메타 데이터 XML hello 또는 인증서를 환영 hello 옵션 toodownload를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-155">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="064e1-156">Azure AD URL tooget hello 메타 데이터를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-156">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="064e1-157">hello 메타 데이터를 XML 파일로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-157">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a><span data-ttu-id="064e1-158">Toocustomize SAML 클레임 tooan 응용 프로그램을 전송 하는 방법을 알 수 없습니다</span><span class="sxs-lookup"><span data-stu-id="064e1-158">Don't know how toocustomize SAML claims sent tooan application</span></span>

<span data-ttu-id="064e1-159">toolearn toocustomize hello SAML 특성 클레임 전송 tooyour 응용 프로그램 참조 [Azure Active Directory에서 매핑을 클레임](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="064e1-159">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="064e1-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="064e1-160">Next steps</span></span>
[<span data-ttu-id="064e1-161">Azure Active Directory로 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="064e1-161">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
