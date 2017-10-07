---
title: "페더레이션된 single sign-on 구성 갤러리가 아닌 응용 프로그램에 대 한 aaaProblem | Microsoft Docs"
description: "페더레이션된 single sign on tooyour 사용자 지정 SAML 응용 프로그램 나열 되어 있지 않은 hello Azure AD 응용 프로그램 갤러리에서에서 구성할 때 발생 하는 hello 일반적인 문제 중 일부를 해결합니다"
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
ms.openlocfilehash: 8c80f0001de01cbc9930ef0441cd804082ee8578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="50332-103">비갤러리 응용 프로그램에 대해 비갤러리 Single Sign-On 구성 문제</span><span class="sxs-lookup"><span data-stu-id="50332-103">Problem configuring federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="50332-104">응용 프로그램을 구성할 때 문제가 발생 할 경우.</span><span class="sxs-lookup"><span data-stu-id="50332-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="50332-105">Hello 문서의 모든 hello 단계를 따랐는지 확인 [single sign on tooapplications hello Azure Active Directory 응용 프로그램 갤러리에 없는 구성 합니다.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span><span class="sxs-lookup"><span data-stu-id="50332-105">Verify you have followed all hello steps in hello article [Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span></span>

## <a name="cant-add-another-instance-of-hello-application"></a><span data-ttu-id="50332-106">Hello 응용 프로그램의 다른 인스턴스를 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="50332-106">Can’t add another instance of hello application</span></span>

<span data-ttu-id="50332-107">응용 프로그램의 두 번째 인스턴스 tooadd 필요한 toobe 수 있습니다:</span><span class="sxs-lookup"><span data-stu-id="50332-107">tooadd a second instance of an application, you need toobe able to:</span></span>

-   <span data-ttu-id="50332-108">Hello 두 번째 인스턴스에 대 한 고유 식별자를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="50332-108">Configure a unique identifier for hello second instance.</span></span> <span data-ttu-id="50332-109">동일한 식별자 사용에 대 한 hello 첫 번째 인스턴스 수 tooconfigure hello 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="50332-109">You won’t be able tooconfigure hello same identifier used for hello first instance.</span></span>

-   <span data-ttu-id="50332-110">첫 번째 인스턴스 hello에 대 한 사용 되는 hello와 다른 인증서를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="50332-110">Configure a different certificate than hello one used for hello first instance.</span></span>

<span data-ttu-id="50332-111">경우 hello 응용 프로그램 hello 위의 중 하나를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="50332-111">If hello application doesn’t support any of hello above.</span></span> <span data-ttu-id="50332-112">그런 다음 두 번째 인스턴스 수 tooconfigure 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="50332-112">Then, you won’t be able tooconfigure a second instance.</span></span>

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a><span data-ttu-id="50332-113">Hello EntityID (사용자 식별자) 형식을 설정 하는 위치</span><span class="sxs-lookup"><span data-stu-id="50332-113">Where do I set hello EntityID (User Identifier) format</span></span>

<span data-ttu-id="50332-114">Azure AD는 hello에 대 한 응답 toohello 응용 프로그램 사용자 인증 후 보냅니다 수 tooselect hello EntityID (사용자 식별자) 형식 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="50332-114">You won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="50332-115">Hello NameID 특성 (사용자 식별자)에 대 한 azure AD 선택 hello 형식 선택한 hello 값에 따라 또는 hello SAML AuthRequest hello에 hello 응용 프로그램에서 요청한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="50332-115">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="50332-116">자세한 내용은 방문 hello 문서 [Single Sign On SAML 프로토콜](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) hello 섹션 NameIDPolicy,</span><span class="sxs-lookup"><span data-stu-id="50332-116">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy,</span></span>

## <a name="where-do-i-get-hello-application-metadata-or-certificate-from-azure-ad"></a><span data-ttu-id="50332-117">여기서 얻는 hello 응용 프로그램 메타 데이터 또는 인증서 Azure AD에서</span><span class="sxs-lookup"><span data-stu-id="50332-117">Where do I get hello application metadata or certificate from Azure AD</span></span>

<span data-ttu-id="50332-118">toodownload hello에 대 한 응용 프로그램 메타 데이터 또는 Azure AD에서 인증서를 다음 hello 단계를 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="50332-118">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="50332-119">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="50332-119">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="50332-120">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50332-120">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="50332-121">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="50332-121">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="50332-122">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="50332-122">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="50332-123">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="50332-123">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="50332-124">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="50332-124">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="50332-125">Single sign on 구성한 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="50332-125">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="50332-126">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="50332-126">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="50332-127">너무 이동**SAML 서명 인증서** 섹션에서 다음 클릭 **다운로드** 열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="50332-127">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="50332-128">어떤 hello 응용 프로그램에 single sign-on 구성 필요한 경우에 따라 메타 데이터 XML hello 또는 인증서를 환영 hello 옵션 toodownload를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50332-128">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="50332-129">Azure AD URL tooget hello 메타 데이터를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="50332-129">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="50332-130">hello 메타 데이터를 XML 파일로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50332-130">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a><span data-ttu-id="50332-131">Toocustomize SAML 클레임 tooan 응용 프로그램을 전송 하는 방법을 알 수 없습니다</span><span class="sxs-lookup"><span data-stu-id="50332-131">Don't know how toocustomize SAML claims sent tooan application</span></span>

<span data-ttu-id="50332-132">toolearn toocustomize hello SAML 특성 클레임 전송 tooyour 응용 프로그램 참조 [Azure Active Directory에서 매핑을 클레임](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="50332-132">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50332-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="50332-133">Next steps</span></span>
[<span data-ttu-id="50332-134">Azure Active Directory로 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="50332-134">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
