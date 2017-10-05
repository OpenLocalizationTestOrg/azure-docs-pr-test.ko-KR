---
title: "Azure AD에서 페더레이션 인증서 관리 | Microsoft Docs"
description: "페더레이션 인증서에 대한 만료 날짜를 사용자 지정하는 방법 및 곧 만료되는 인증서를 갱신하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f516f7f0-b25a-4901-8247-f5964666ce23
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/09/2017
ms.author: jeedes
ms.openlocfilehash: 1283b570200f05003658824760ecbb6722f241d9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-certificates-for-federated-single-sign-on-in-azure-active-directory"></a><span data-ttu-id="38c22-103">Azure Active Directory에서 페더레이션된 Single Sign-On에 대한 인증서 관리</span><span class="sxs-lookup"><span data-stu-id="38c22-103">Manage certificates for federated single sign-on in Azure Active Directory</span></span>
<span data-ttu-id="38c22-104">이 문서에서는 Azure AD(Azure Active Directory)에서 SaaS 응용 프로그램에 페더레이션된 SSO(Single Sign-On)를 설정하기 위해 만드는 인증서와 관련된 일반적인 질문과 정보를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-104">This article covers common questions and information related to the certificates that Azure Active Directory (Azure AD) creates to establish federated single sign-on (SSO) to your SaaS applications.</span></span> <span data-ttu-id="38c22-105">Azure AD 앱 갤러리에서 또는 비갤러리 응용 프로그램 템플릿을 사용하여 응용 프로그램을 추가하고,</span><span class="sxs-lookup"><span data-stu-id="38c22-105">Add applications from the Azure AD app gallery or by using a non-gallery application template.</span></span> <span data-ttu-id="38c22-106">페더레이션된 SSO 옵션을 사용하여 응용 프로그램을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-106">Configure the application by using the federated SSO option.</span></span>

<span data-ttu-id="38c22-107">이 문서는 아래 예와 같이 SAML 페더레이션을 통해 Azure AD SSO를 사용하도록 구성된 앱에만 관련되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-107">This article is relevant only to apps that are configured to use Azure AD SSO through SAML federation, as shown in the following example:</span></span>

![Azure AD Single Sign-On](./media/active-directory-sso-certs/saml_sso.PNG)

## <a name="auto-generated-certificate-for-gallery-and-non-gallery-applications"></a><span data-ttu-id="38c22-109">갤러리 및 비갤러리 응용 프로그램에 대해 자동 생성된 인증서</span><span class="sxs-lookup"><span data-stu-id="38c22-109">Auto-generated certificate for gallery and non-gallery applications</span></span>
<span data-ttu-id="38c22-110">갤러리에서 새 응용 프로그램을 추가하고 SAML 기반 로그온을 구성하면 Azure AD에서 해당 응용 프로그램에 대해 3년 동안 유효한 인증서를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-110">When you add a new application from the gallery and configure a SAML-based sign-on, Azure AD generates a certificate for the application that is valid for three years.</span></span> <span data-ttu-id="38c22-111">이 인증서는 **SAML 서명 인증서** 섹션에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-111">You can download this certificate from the **SAML Signing Certificate** section.</span></span> <span data-ttu-id="38c22-112">갤러리 응용 프로그램의 경우 이 섹션에서는 응용 프로그램의 요구 사항에 따라 인증서 또는 메타데이터를 다운로드하는 옵션을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-112">For gallery applications, this section might show an option to download the certificate or metadata, depending on the requirement of the application.</span></span>

![Azure AD Single Sign-On](./media/active-directory-sso-certs/saml_certificate_download.png)

## <a name="customize-the-expiration-date-for-your-federation-certificate-and-roll-it-over-to-a-new-certificate"></a><span data-ttu-id="38c22-114">페더레이션 인증서의 만료 날짜 사용자 지정 및 새 인증서 롤오버</span><span class="sxs-lookup"><span data-stu-id="38c22-114">Customize the expiration date for your federation certificate and roll it over to a new certificate</span></span>
<span data-ttu-id="38c22-115">기본적으로 인증서는 3년 후에 만료되도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-115">By default, certificates are set to expire after three years.</span></span> <span data-ttu-id="38c22-116">다음 단계를 완료하여 인증서의 다른 만료 날짜를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-116">You can choose a different expiration date for your certificate by completing the following steps.</span></span>
<span data-ttu-id="38c22-117">스크린샷에서는 예제를 위해 Salesforce를 사용하지만, 이러한 단계는 페더레이션된 모든 SaaS 앱에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-117">The screenshots use Salesforce for the sake of example, but these steps can apply to any federated SaaS app.</span></span>

1. <span data-ttu-id="38c22-118">[Azure Portal](https://aad.portal.azure.com)의 왼쪽 창에서 **엔터프라이즈 응용 프로그램**을 클릭한 다음 **개요** 페이지에서 **새 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-118">In the [Azure portal](https://aad.portal.azure.com), click **Enterprise application** in the left pane and then click **New application** on the **Overview** page:</span></span>

   ![SSO 구성 마법사 열기](./media/active-directory-sso-certs/enterprise_application_new_application.png)

2. <span data-ttu-id="38c22-120">갤러리 응용 프로그램을 검색한 다음 추가할 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-120">Search for the gallery application and then select the application that you want to add.</span></span> <span data-ttu-id="38c22-121">필요한 응용 프로그램을 찾을 수 없으면 **비갤러리 응용 프로그램** 옵션을 사용하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-121">If you cannot find the required application, add the application by using the **Non-gallery application** option.</span></span> <span data-ttu-id="38c22-122">이 기능은 Azure AD Premium(P1 및 P2) SKU에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-122">This feature is available only in the Azure AD Premium (P1 and P2) SKU.</span></span>

    ![Azure AD Single Sign-On](./media/active-directory-sso-certs/add_gallery_application.png)

3. <span data-ttu-id="38c22-124">왼쪽 창에서 **Single Sign-On** 링크를 클릭하고 **Single Sign-On 모드**를 **SAML 기반 로그인**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-124">Click the **Single sign-on** link in the left pane and change **Single Sign-on Mode** to **SAML-based Sign-on**.</span></span> <span data-ttu-id="38c22-125">이 단계에서는 응용 프로그램에 대해 3년 유효 인증서를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-125">This step generates a three-year certificate for your application.</span></span>

4. <span data-ttu-id="38c22-126">새 인증서를 만들려면 **SAML 서명 인증서** 섹션에서 **새 인증서 만들기** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-126">To create a new certificate, click the **Create new certificate** link in the **SAML Signing Certificate** section.</span></span>

    ![새 인증서 생성](./media/active-directory-sso-certs/create_new_certficate.png)

5. <span data-ttu-id="38c22-128">**새 인증서 만들기** 링크는 달력 컨트롤을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-128">The **Create a new certificate** link opens the calendar control.</span></span> <span data-ttu-id="38c22-129">날짜와 시간은 현재 날짜로부터 최대 3년까지 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-129">You can set any date and time up to three years from the current date.</span></span> <span data-ttu-id="38c22-130">선택한 날짜와 시간은 새 인증서의 새로운 만료 날짜와 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-130">The selected date and time is the new expiration date and time of your new certificate.</span></span> <span data-ttu-id="38c22-131">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-131">Click **Save**.</span></span>

    ![다운로드한 다음 인증서 업로드](./media/active-directory-sso-certs/certifcate_date_selection.PNG)

6. <span data-ttu-id="38c22-133">이제 새 인증서를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-133">Now the new certificate is available to download.</span></span> <span data-ttu-id="38c22-134">**인증서** 링크를 클릭하여 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-134">Click the **Certificate** link to download it.</span></span> <span data-ttu-id="38c22-135">이 시점에서 인증서는 활성 상태가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-135">At this point, your certificate is not active.</span></span> <span data-ttu-id="38c22-136">이 인증서를 롤오버하려면 **Make new certificate active**(새 인증서 활성화) 확인란을 선택하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-136">When you want to roll over to this certificate, select the **Make new certificate active** check box and click **Save**.</span></span> <span data-ttu-id="38c22-137">이 시점부터 Azure AD에서 새 인증서를 사용하여 응답에 서명하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-137">From that point, Azure AD starts using the new certificate for signing the response.</span></span>

7.  <span data-ttu-id="38c22-138">특정 SaaS 응용 프로그램에 인증서를 업로드하는 방법을 알아보려면 **응용 프로그램 구성 자습서 보기** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-138">To learn how to upload the certificate to your particular SaaS application, click the **View application configuration tutorial** link.</span></span>

## <a name="renew-a-certificate-that-will-soon-expire"></a><span data-ttu-id="38c22-139">곧 만료되는 인증서 갱신</span><span class="sxs-lookup"><span data-stu-id="38c22-139">Renew a certificate that will soon expire</span></span>
<span data-ttu-id="38c22-140">다음 갱신 단계를 수행하면 사용자에게 심각한 가동 중지가 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-140">The following renewal steps should result in no significant downtime for your users.</span></span> <span data-ttu-id="38c22-141">이 섹션의 스크린샷에서는 Salesforce를 예로 사용하지만, 이러한 단계는 페더레이션된 모든 SaaS 앱에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-141">The screenshots in this section feature Salesforce as an example, but these steps can apply to any federated SaaS app.</span></span>

1. <span data-ttu-id="38c22-142">**Azure Active Directory** 응용 프로그램 **Single Sign-On** 페이지에서 응용 프로그램에 대한 새 인증서를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-142">On the **Azure Active Directory** application **Single sign-on** page, generate the new certificate for your application.</span></span> <span data-ttu-id="38c22-143">**SAML 서명 인증서** 섹션에서 **새 인증서 만들기** 링크를 클릭하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-143">You can do this by clicking the **Create new certificate** link in the **SAML Signing Certificate** section.</span></span>

    ![새 인증서 생성](./media/active-directory-sso-certs/create_new_certficate.png)

2. <span data-ttu-id="38c22-145">새 인증서에 대해 원하는 만료 날짜와 시간을 선택하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-145">Select the desired expiration date and time for your new certificate and click **Save**.</span></span>

3. <span data-ttu-id="38c22-146">**SAML 서명 인증서** 옵션에서 인증서를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-146">Download the certificate in the **SAML Signing certificate** option.</span></span> <span data-ttu-id="38c22-147">새 인증서를 SaaS 응용 프로그램의 Single Sign-On 구성 화면에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-147">Upload the new certificate to the SaaS application's single sign-on configuration screen.</span></span> <span data-ttu-id="38c22-148">특정 SaaS 응용 프로그램에 대해 이 작업을 수행하는 방법을 알아보려면 **응용 프로그램 구성 자습서 보기** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-148">To learn how to do this for your particular SaaS application, click the **View application configuration tutorial** link.</span></span>
   
4. <span data-ttu-id="38c22-149">Azure AD에서 새 인증서를 활성화하려면 **Make new certificate active**(새 인증서 활성화) 확인란을 선택하고 페이지 위쪽에서 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-149">To activate the new certificate in Azure AD, select the **Make new certificate active** check box and click the **Save** button at the top of the page.</span></span> <span data-ttu-id="38c22-150">그러면 Azure AD 쪽에서 새 인증서를 롤오버합니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-150">This rolls over the new certificate on the Azure AD side.</span></span> <span data-ttu-id="38c22-151">인증서의 상태가 **신규**에서 **활성**으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-151">The status of the certificate changes from **New** to **Active**.</span></span> <span data-ttu-id="38c22-152">이 시점부터 Azure AD에서 새 인증서를 사용하여 응답에 서명하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="38c22-152">From that point, Azure AD starts using the new certificate for signing the response.</span></span> 
   
    ![새 인증서 생성](./media/active-directory-sso-certs/new_certificate_download.png)

## <a name="related-articles"></a><span data-ttu-id="38c22-154">관련 문서</span><span class="sxs-lookup"><span data-stu-id="38c22-154">Related articles</span></span>
* [<span data-ttu-id="38c22-155">Azure Active Directory를 사용하여 SaaS 앱을 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="38c22-155">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="38c22-156">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="38c22-156">Article index for application management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="38c22-157">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="38c22-157">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="38c22-158">SAML 기반 Single Sign-On 문제 해결</span><span class="sxs-lookup"><span data-stu-id="38c22-158">Troubleshooting SAML-based single sign-on</span></span>](active-directory-saml-debugging.md)
