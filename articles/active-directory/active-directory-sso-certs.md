---
title: "Azure AD의 페더레이션 인증서 aaaManage | Microsoft Docs"
description: "어떻게 toorenew 인증서는 페더레이션 인증서에 사용 되는 hello 만료 날짜 toocustomize 곧 만료 방법에 대해 알아봅니다."
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
ms.openlocfilehash: e17622d25c9babfa295cc0bb68c24e21b8c574d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-certificates-for-federated-single-sign-on-in-azure-active-directory"></a><span data-ttu-id="e27a3-103">Azure Active Directory에서 페더레이션된 Single Sign-On에 대한 인증서 관리</span><span class="sxs-lookup"><span data-stu-id="e27a3-103">Manage certificates for federated single sign-on in Azure Active Directory</span></span>
<span data-ttu-id="e27a3-104">이 문서에서는 일반적인 질문 및 Azure Active Directory (Azure AD) tooestablish 만들어지는 toohello 인증서 페더레이션된 single sign-on (SSO) tooyour SaaS 응용 프로그램 관련 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-104">This article covers common questions and information related toohello certificates that Azure Active Directory (Azure AD) creates tooestablish federated single sign-on (SSO) tooyour SaaS applications.</span></span> <span data-ttu-id="e27a3-105">Hello Azure AD 앱 갤러리에서 또는 비 갤러리 응용 프로그램 템플릿을 사용 하 여 응용 프로그램을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-105">Add applications from hello Azure AD app gallery or by using a non-gallery application template.</span></span> <span data-ttu-id="e27a3-106">Hello 페더레이션 SSO 옵션을 사용 하 여 hello 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-106">Configure hello application by using hello federated SSO option.</span></span>

<span data-ttu-id="e27a3-107">이 문서는 있는 통해 SAML 페더레이션 구성된 toouse Azure AD SSO 관련만 tooapps hello 다음 예제와 같이:</span><span class="sxs-lookup"><span data-stu-id="e27a3-107">This article is relevant only tooapps that are configured toouse Azure AD SSO through SAML federation, as shown in hello following example:</span></span>

![Azure AD Single Sign-On](./media/active-directory-sso-certs/saml_sso.PNG)

## <a name="auto-generated-certificate-for-gallery-and-non-gallery-applications"></a><span data-ttu-id="e27a3-109">갤러리 및 비갤러리 응용 프로그램에 대해 자동 생성된 인증서</span><span class="sxs-lookup"><span data-stu-id="e27a3-109">Auto-generated certificate for gallery and non-gallery applications</span></span>
<span data-ttu-id="e27a3-110">Hello 갤러리에서 새 응용 프로그램을 추가 하는 SAML 기반 로그온을 구성 하는 경우 Azure AD는 3 년 동안 유효 하는 hello 응용 프로그램에 대 한 인증서를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-110">When you add a new application from hello gallery and configure a SAML-based sign-on, Azure AD generates a certificate for hello application that is valid for three years.</span></span> <span data-ttu-id="e27a3-111">Hello에서이 인증서를 다운로드할 수 있습니다 **SAML 서명 인증서** 섹션.</span><span class="sxs-lookup"><span data-stu-id="e27a3-111">You can download this certificate from hello **SAML Signing Certificate** section.</span></span> <span data-ttu-id="e27a3-112">갤러리 응용 프로그램에 대 한이 섹션은 옵션 toodownload hello 인증서 또는 hello 응용 프로그램의 hello 요구 사항에 따라 메타 데이터를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-112">For gallery applications, this section might show an option toodownload hello certificate or metadata, depending on hello requirement of hello application.</span></span>

![Azure AD Single Sign-On](./media/active-directory-sso-certs/saml_certificate_download.png)

## <a name="customize-hello-expiration-date-for-your-federation-certificate-and-roll-it-over-tooa-new-certificate"></a><span data-ttu-id="e27a3-114">페더레이션 인증서에 대 한 hello 만료 날짜를 사용자 지정 하 고 tooa 새 인증서 롤오버</span><span class="sxs-lookup"><span data-stu-id="e27a3-114">Customize hello expiration date for your federation certificate and roll it over tooa new certificate</span></span>
<span data-ttu-id="e27a3-115">인증서는 기본적으로 3 년 후 tooexpire를 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-115">By default, certificates are set tooexpire after three years.</span></span> <span data-ttu-id="e27a3-116">Hello 다음 단계를 완료 하 여 인증서에 대 한 다른 만료 날짜를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-116">You can choose a different expiration date for your certificate by completing hello following steps.</span></span>
<span data-ttu-id="e27a3-117">hello 스크린샷에서 Salesforce 등의 hello 위해서 사용 하 여 하지만 다음이 단계는 tooany 페더레이션 SaaS 응용 프로그램을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-117">hello screenshots use Salesforce for hello sake of example, but these steps can apply tooany federated SaaS app.</span></span>

1. <span data-ttu-id="e27a3-118">Hello에 [Azure 포털](https://aad.portal.azure.com), 클릭 **엔터프라이즈 응용 프로그램** 왼쪽된 창의 hello와 클릭 **새 응용 프로그램** hello에 **개요** 페이지:</span><span class="sxs-lookup"><span data-stu-id="e27a3-118">In hello [Azure portal](https://aad.portal.azure.com), click **Enterprise application** in hello left pane and then click **New application** on hello **Overview** page:</span></span>

   ![열기 hello SSO 구성 마법사](./media/active-directory-sso-certs/enterprise_application_new_application.png)

2. <span data-ttu-id="e27a3-120">Hello 갤러리 응용 프로그램에 대 한 검색 하 고 원하는 tooadd hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-120">Search for hello gallery application and then select hello application that you want tooadd.</span></span> <span data-ttu-id="e27a3-121">Hello 필요한 응용 프로그램을 찾을 수 없으면 hello를 사용 하 여 hello 응용 프로그램을 추가 **비 갤러리 응용 프로그램** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-121">If you cannot find hello required application, add hello application by using hello **Non-gallery application** option.</span></span> <span data-ttu-id="e27a3-122">이 기능은 Azure AD Premium (P1 및 P2) SKU hello 에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-122">This feature is available only in hello Azure AD Premium (P1 and P2) SKU.</span></span>

    ![Azure AD Single Sign-On](./media/active-directory-sso-certs/add_gallery_application.png)

3. <span data-ttu-id="e27a3-124">Hello 클릭 **Single sign on** 링크의 왼쪽 창에서 데이터 및 변경 하는 hello **Single Sign on 모드** 너무**SAML 기반 로그온**합니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-124">Click hello **Single sign-on** link in hello left pane and change **Single Sign-on Mode** too**SAML-based Sign-on**.</span></span> <span data-ttu-id="e27a3-125">이 단계에서는 응용 프로그램에 대해 3년 유효 인증서를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-125">This step generates a three-year certificate for your application.</span></span>

4. <span data-ttu-id="e27a3-126">새 인증서를 toocreate 클릭 hello **새 인증서 만들기** hello에 대 한 링크 **SAML 서명 인증서** 섹션.</span><span class="sxs-lookup"><span data-stu-id="e27a3-126">toocreate a new certificate, click hello **Create new certificate** link in hello **SAML Signing Certificate** section.</span></span>

    ![새 인증서 생성](./media/active-directory-sso-certs/create_new_certficate.png)

5. <span data-ttu-id="e27a3-128">hello **새 인증서를 만들** 링크 hello 달력 컨트롤을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-128">hello **Create a new certificate** link opens hello calendar control.</span></span> <span data-ttu-id="e27a3-129">에서 설정할 수 있습니다 날짜 및 시간을 toothree 년 hello 현재 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-129">You can set any date and time up toothree years from hello current date.</span></span> <span data-ttu-id="e27a3-130">hello 날짜를 선택 하 고 새로운 만료 날짜로 hello와 새 인증서의 시간 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-130">hello selected date and time is hello new expiration date and time of your new certificate.</span></span> <span data-ttu-id="e27a3-131">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-131">Click **Save**.</span></span>

    ![다운로드 한 다음 hello 인증서 업로드](./media/active-directory-sso-certs/certifcate_date_selection.PNG)

6. <span data-ttu-id="e27a3-133">이제 hello 새 인증서는 사용할 수 있는 toodownload입니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-133">Now hello new certificate is available toodownload.</span></span> <span data-ttu-id="e27a3-134">Hello 클릭 **인증서** 링크 toodownload 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-134">Click hello **Certificate** link toodownload it.</span></span> <span data-ttu-id="e27a3-135">이 시점에서 인증서는 활성 상태가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-135">At this point, your certificate is not active.</span></span> <span data-ttu-id="e27a3-136">Toothis 인증서를 통해 tooroll 하려는 경우 선택 hello **새 인증서를 활성화할** 확인란과 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-136">When you want tooroll over toothis certificate, select hello **Make new certificate active** check box and click **Save**.</span></span> <span data-ttu-id="e27a3-137">해당 시점에서 Azure AD 서명 hello 응답에 대 한 hello 새 인증서를 사용 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-137">From that point, Azure AD starts using hello new certificate for signing hello response.</span></span>

7.  <span data-ttu-id="e27a3-138">toolearn tooupload hello tooyour 특정 SaaS 응용 프로그램 인증서 방법 클릭 hello **보기 응용 프로그램 구성 자습서** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-138">toolearn how tooupload hello certificate tooyour particular SaaS application, click hello **View application configuration tutorial** link.</span></span>

## <a name="renew-a-certificate-that-will-soon-expire"></a><span data-ttu-id="e27a3-139">곧 만료되는 인증서 갱신</span><span class="sxs-lookup"><span data-stu-id="e27a3-139">Renew a certificate that will soon expire</span></span>
<span data-ttu-id="e27a3-140">hello 다음 갱신 단계를 유발 사용자에 게 중요 한 중단 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-140">hello following renewal steps should result in no significant downtime for your users.</span></span> <span data-ttu-id="e27a3-141">예를 들어 있지만 이러한 단계가이 섹션 기능 Salesforce에서에서 hello 스크린 샷 tooany 페더레이션 SaaS 응용 프로그램을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-141">hello screenshots in this section feature Salesforce as an example, but these steps can apply tooany federated SaaS app.</span></span>

1. <span data-ttu-id="e27a3-142">Hello에 **Azure Active Directory** 응용 프로그램 **Single sign on** 페이지에서 응용 프로그램에 대 한 hello 새 인증서를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-142">On hello **Azure Active Directory** application **Single sign-on** page, generate hello new certificate for your application.</span></span> <span data-ttu-id="e27a3-143">Hello를 클릭 하 여이 작업을 수행할 수 **새 인증서 만들기** hello에 대 한 링크 **SAML 서명 인증서** 섹션.</span><span class="sxs-lookup"><span data-stu-id="e27a3-143">You can do this by clicking hello **Create new certificate** link in hello **SAML Signing Certificate** section.</span></span>

    ![새 인증서 생성](./media/active-directory-sso-certs/create_new_certficate.png)

2. <span data-ttu-id="e27a3-145">만료 날짜와 새 인증서에 해당 시간 선택 hello 원하는 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-145">Select hello desired expiration date and time for your new certificate and click **Save**.</span></span>

3. <span data-ttu-id="e27a3-146">Hello에 hello 인증서 다운로드 **SAML 서명 인증서** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-146">Download hello certificate in hello **SAML Signing certificate** option.</span></span> <span data-ttu-id="e27a3-147">Hello 새 인증서 toohello SaaS 응용 프로그램의 single sign on 구성 화면을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-147">Upload hello new certificate toohello SaaS application's single sign-on configuration screen.</span></span> <span data-ttu-id="e27a3-148">toolearn 어떻게 toodo 특정 SaaS 응용 프로그램에 대 한이 클릭 hello **보기 응용 프로그램 구성 자습서** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-148">toolearn how toodo this for your particular SaaS application, click hello **View application configuration tutorial** link.</span></span>
   
4. <span data-ttu-id="e27a3-149">Azure ad에서는 선택 hello tooactivate hello 새 인증서 **새 인증서를 활성화할** 확인란을 클릭 hello **저장** hello hello 페이지 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-149">tooactivate hello new certificate in Azure AD, select hello **Make new certificate active** check box and click hello **Save** button at hello top of hello page.</span></span> <span data-ttu-id="e27a3-150">이 hello 새 인증서를 통해 Azure AD 쪽 hello에 롤업합니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-150">This rolls over hello new certificate on hello Azure AD side.</span></span> <span data-ttu-id="e27a3-151">hello 인증서의 hello 상태에서 변경 **새로** 너무**활성**합니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-151">hello status of hello certificate changes from **New** too**Active**.</span></span> <span data-ttu-id="e27a3-152">해당 시점에서 Azure AD 서명 hello 응답에 대 한 hello 새 인증서를 사용 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e27a3-152">From that point, Azure AD starts using hello new certificate for signing hello response.</span></span> 
   
    ![새 인증서 생성](./media/active-directory-sso-certs/new_certificate_download.png)

## <a name="related-articles"></a><span data-ttu-id="e27a3-154">관련 문서</span><span class="sxs-lookup"><span data-stu-id="e27a3-154">Related articles</span></span>
* [<span data-ttu-id="e27a3-155">방법에 대 한 자습서 목록 toointegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="e27a3-155">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e27a3-156">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="e27a3-156">Article index for application management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="e27a3-157">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e27a3-157">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="e27a3-158">SAML 기반 Single Sign-On 문제 해결</span><span class="sxs-lookup"><span data-stu-id="e27a3-158">Troubleshooting SAML-based single sign-on</span></span>](active-directory-saml-debugging.md)
