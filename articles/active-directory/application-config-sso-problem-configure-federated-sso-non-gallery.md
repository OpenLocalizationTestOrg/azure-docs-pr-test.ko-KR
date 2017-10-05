---
title: "비갤러리 응용 프로그램에 대해 비갤러리 Single Sign-On 구성 문제 | Microsoft Docs"
description: "Azure AD 응용 프로그램 갤러리에 나열되지 않은 사용자 지정 SAML 응용 프로그램에 페더레이션된 Single Sign-On을 구성할 때 발생하는 일반적인 문제 몇 가지를 해결"
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
ms.openlocfilehash: 4eb2c04c940dd6ad15a491a331aed76c237f0387
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="0c15b-103">비갤러리 응용 프로그램에 대해 비갤러리 Single Sign-On 구성 문제</span><span class="sxs-lookup"><span data-stu-id="0c15b-103">Problem configuring federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="0c15b-104">응용 프로그램을 구성할 때 문제가 발생 할 경우.</span><span class="sxs-lookup"><span data-stu-id="0c15b-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="0c15b-105">[Azure Active Directory 응용 프로그램 갤러리에 있지 않은 응용 프로그램에 Single Sign-On 구성](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps) 문서에 있는 단계를 모두 수행했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0c15b-105">Verify you have followed all the steps in the article [Configuring single sign-on to applications that are not in the Azure Active Directory application gallery.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span></span>

## <a name="cant-add-another-instance-of-the-application"></a><span data-ttu-id="0c15b-106">응용 프로그램의 다른 인스턴스를 추가할 수 없음</span><span class="sxs-lookup"><span data-stu-id="0c15b-106">Can’t add another instance of the application</span></span>

<span data-ttu-id="0c15b-107">응용 프로그램의 두 번째 인스턴스를 추가하려면 다음을 수행할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c15b-107">To add a second instance of an application, you need to be able to:</span></span>

-   <span data-ttu-id="0c15b-108">두 번째 인스턴스에 대한 고유 식별자를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0c15b-108">Configure a unique identifier for the second instance.</span></span> <span data-ttu-id="0c15b-109">첫 번째 인스턴스에 대해 사용한 것과 동일한 식별자를 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0c15b-109">You won’t be able to configure the same identifier used for the first instance.</span></span>

-   <span data-ttu-id="0c15b-110">첫 번째 인스턴스에 대해 사용한 것과 다른 인증서를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0c15b-110">Configure a different certificate than the one used for the first instance.</span></span>

<span data-ttu-id="0c15b-111">응용 프로그램에서 위 사항 중에서 어느 것도 지원하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="0c15b-111">If the application doesn’t support any of the above.</span></span> <span data-ttu-id="0c15b-112">두 번째 인스턴스를 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0c15b-112">Then, you won’t be able to configure a second instance.</span></span>

## <a name="where-do-i-set-the-entityid-user-identifier-format"></a><span data-ttu-id="0c15b-113">EntityID(사용자 식별자) 형식을 설정하는 위치</span><span class="sxs-lookup"><span data-stu-id="0c15b-113">Where do I set the EntityID (User Identifier) format</span></span>

<span data-ttu-id="0c15b-114">사용자 인증 후에 Azure AD에서 응답을 통해 응용 프로그램으로 보내는 EntityID(사용자 식별자) 형식은 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0c15b-114">You won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="0c15b-115">Azure AD에서는 선택한 값 또는 SAML AuthRequest에서 응용 프로그램이 요청한 형식을 기반으로 NameID 특성(사용자 식별자)의 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0c15b-115">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="0c15b-116">자세한 내용은 NameIDPolicy 섹션 아래의 [Single Sign-On SAML 프로토콜](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) 문서에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c15b-116">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy,</span></span>

## <a name="where-do-i-get-the-application-metadata-or-certificate-from-azure-ad"></a><span data-ttu-id="0c15b-117">Azure AD에서 응용 프로그램 메타데이터 또는 인증서를 가져오는 위치</span><span class="sxs-lookup"><span data-stu-id="0c15b-117">Where do I get the application metadata or certificate from Azure AD</span></span>

<span data-ttu-id="0c15b-118">Azure AD에서 응용 프로그램 메타데이터 또는 인증서를 다운로드하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0c15b-118">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="0c15b-119">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0c15b-119">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="0c15b-120">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0c15b-120">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0c15b-121">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0c15b-121">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0c15b-122">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0c15b-122">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0c15b-123">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="0c15b-123">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="0c15b-124">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0c15b-124">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="0c15b-125">Single Sign-On을 구성한 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0c15b-125">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="0c15b-126">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0c15b-126">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="0c15b-127">**SAML 서명 인증서** 섹션으로 이동한 다음 **다운로드** 열 값을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0c15b-127">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="0c15b-128">Single Sign-On을 구성해야 할 응용 프로그램에 따라 메타데이터 XML이나 인증서를 다운로드하는 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c15b-128">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="0c15b-129">Azure AD에서는 메타데이터를 가져오는 URL을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0c15b-129">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="0c15b-130">메타데이터는 XML 파일로만 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c15b-130">The metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-to-customize-saml-claims-sent-to-an-application"></a><span data-ttu-id="0c15b-131">응용 프로그램에 전송된 SAML 클레임을 사용자 지정하는 방법을 알 수 없음</span><span class="sxs-lookup"><span data-stu-id="0c15b-131">Don't know how to customize SAML claims sent to an application</span></span>

<span data-ttu-id="0c15b-132">응용 프로그램에 전송된 SAML 특성 클레임을 사용자 지정하는 방법을 알아보려면 [Azure Active Directory의 클레임 매핑](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0c15b-132">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c15b-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0c15b-133">Next steps</span></span>
[<span data-ttu-id="0c15b-134">Azure Active Directory로 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="0c15b-134">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
