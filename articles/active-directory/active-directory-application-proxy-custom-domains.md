---
title: "Azure AD 응용 프로그램 프록시의 사용자 지정 도메인 | Microsoft Docs"
description: "앱의 URL이 사용자가 액세스하는 위치에 관계 없이 동일하도록 Azure AD 응용 프로그램 프록시에서 사용자 지정 도메인을 관리합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2fe9f895-f641-4362-8b27-7a5d08f8600f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 1dde300780c8d1f7ea9eee4c92de06bcf70a1f12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a><span data-ttu-id="33a35-103">Azure AD 응용 프로그램 프록시에서 사용자 지정 도메인 작업</span><span class="sxs-lookup"><span data-stu-id="33a35-103">Working with custom domains in Azure AD Application Proxy</span></span>

<span data-ttu-id="33a35-104">Azure Active Directory 응용 프로그램 프록시를 통해 응용 프로그램을 게시할 때 사용자가 원격으로 작업 중일 때 이동하도록 외부 URL을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-104">When you publish an application through Azure Active Directory Application Proxy, you create an external URL for your users to go to when they're working remotely.</span></span> <span data-ttu-id="33a35-105">이 URL은 기본 도메인 *yourtenant.msappproxy.net*을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-105">This URL gets the default domain *yourtenant.msappproxy.net*.</span></span> <span data-ttu-id="33a35-106">예를 들어 Expenses라는 앱을 게시한 경우 테넌트는 Contoso로 이름이 지정된 다음 외부 URL은 https://expenses-contoso.msappproxy.net이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-106">For example, if you published an app named Expenses and your tenant is named Contoso, then the external URL would be https://expenses-contoso.msappproxy.net.</span></span> <span data-ttu-id="33a35-107">자신의 도메인 이름을 사용하려는 경우 응용 프로그램에 대한 사용자 지정 도메인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-107">If you want to use your own domain name, configure a custom domain for your application.</span></span> 

<span data-ttu-id="33a35-108">언제나 가능한 응용 프로그램에 대한 사용자 지정 도메인을 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-108">We recommend that you set up custom domains for your applications whenever possible.</span></span> <span data-ttu-id="33a35-109">사용자 지정 도메인의 이점 중 일부는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-109">Some of the benefits of custom domains include:</span></span>

- <span data-ttu-id="33a35-110">사용자가 네트워크 내부 또는 외부에서 근무하든지 동일한 URL을 사용하여 응용 프로그램에 접근할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-110">Your users can get to the application with the same URL, whether they are working inside or outside of your network.</span></span>
- <span data-ttu-id="33a35-111">모든 응용 프로그램이 동일한 내부 및 외부 URL을 갖는 경우 다른 응용 프로그램을 가리키는 하나의 응용 프로그램의 링크는 회사 네트워크 외부에서도 계속해서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-111">If all of your applications have the same internal and external URLs, then links in one application that point to another continue to work even outside the corporate network.</span></span> 
- <span data-ttu-id="33a35-112">브랜딩을 제어하고 원하는 URL을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-112">You control your branding, and create the URLs you want.</span></span> 


## <a name="configure-a-custom-domain"></a><span data-ttu-id="33a35-113">사용자 지정 도메인 구성</span><span class="sxs-lookup"><span data-stu-id="33a35-113">Configure a custom domain</span></span>

### <a name="prerequisites"></a><span data-ttu-id="33a35-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="33a35-114">Prerequisites</span></span>

<span data-ttu-id="33a35-115">사용자 지정 도메인을 구성하기 전에 다음 요구 사항이 준비되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-115">Before you configure a custom domain, make sure that you have the following requirements prepared:</span></span> 
- <span data-ttu-id="33a35-116">[Azure Active Directory에 추가된 확인된 도메인](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="33a35-116">A [verified domain added to Azure Active Directory](active-directory-domains-add-azure-portal.md).</span></span>
- <span data-ttu-id="33a35-117">PFX 파일 형태의 도메인에 대한 사용자 지정 인증서.</span><span class="sxs-lookup"><span data-stu-id="33a35-117">A custom certificate for the domain, in the form of a PFX file.</span></span> 
- <span data-ttu-id="33a35-118">[응용 프로그램 프록시를 통해 게시된](application-proxy-publish-azure-portal.md) 온-프레미스 앱.</span><span class="sxs-lookup"><span data-stu-id="33a35-118">An on-premises app [published through Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

### <a name="configure-your-custom-domain"></a><span data-ttu-id="33a35-119">사용자 지정 도메인 구성</span><span class="sxs-lookup"><span data-stu-id="33a35-119">Configure your custom domain</span></span>

<span data-ttu-id="33a35-120">이러한 세 가지 요구 사항을 준비한 경우 다음 단계를 따라 사용자 지정 도메인을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-120">When you have those three requirements ready, follow these steps to set up your custom domain:</span></span>

1. <span data-ttu-id="33a35-121">[Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-121">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="33a35-122">**Azure Active Directory** > **Enterprise 응용 프로그램** > **모든 응용 프로그램**으로 이동하고 관리하려는 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-122">Navigate to **Azure Active Directory** > **Enterprise applications** > **All applications** and choose the app you want to manage.</span></span>
3. <span data-ttu-id="33a35-123">**응용 프로그램 프록시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-123">Select **Application Proxy**.</span></span> 
4. <span data-ttu-id="33a35-124">외부 URL 필드에서 드롭다운 목록을 사용하여 사용자 지정 도메인을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-124">In the External URL field, use the dropdown list to select your custom domain.</span></span> <span data-ttu-id="33a35-125">목록에서 도메인이 보이지 않는 경우 아직 확인되지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-125">If you don't see your domain in the list, then it hasn't been verified yet.</span></span> 
5. <span data-ttu-id="33a35-126">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-126">Select **Save**</span></span>
5. <span data-ttu-id="33a35-127">비활성화되었던 **인증서** 필드가 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-127">The **Certificate** field that was disabled becomes enabled.</span></span> <span data-ttu-id="33a35-128">이 필드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-128">Select this field.</span></span> 

   ![인증서를 업로드하려면 클릭](./media/active-directory-application-proxy-custom-domains/certificate.png)

   <span data-ttu-id="33a35-130">이 도메인에 대한 인증서를 이미 업로드한 경우 인증서 필드에는 인증서 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-130">If you already uploaded a certificate for this domain, the Certificate field displays the certificate information.</span></span> 

6. <span data-ttu-id="33a35-131">PFX 인증서를 업로드하고 인증서의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-131">Upload the PFX certificate and enter the password for the certificate.</span></span> 
7. <span data-ttu-id="33a35-132">**저장**을 선택하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-132">Select **Save** to save your changes.</span></span> 
8. <span data-ttu-id="33a35-133">msappproxy.net 도메인에 새 외부 URL을 리디렉션하는 [DNS 레코드](../dns/dns-operations-recordsets-portal.md)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-133">Add a [DNS record](../dns/dns-operations-recordsets-portal.md) that redirects the new external URL to the msappproxy.net domain.</span></span> 

>[!TIP] 
><span data-ttu-id="33a35-134">사용자 지정 도메인당 하나의 인증서를 업로드하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-134">You only need to upload one certificate per custom domain.</span></span> <span data-ttu-id="33a35-135">인증서를 업로드한 후 새 앱을 게시하고 DNS 레코드를 제외하고 추가 구성을 수행할 필요가 없는 경우 사용자 지정 도메인을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-135">Once you upload a certificate, you can choose the custom domain when you publish a new app and not have to do additional configuration except for the DNS record.</span></span> 

## <a name="manage-certificates"></a><span data-ttu-id="33a35-136">인증서 관리</span><span class="sxs-lookup"><span data-stu-id="33a35-136">Manage certificates</span></span>

### <a name="certificate-format"></a><span data-ttu-id="33a35-137">인증서 형식</span><span class="sxs-lookup"><span data-stu-id="33a35-137">Certificate format</span></span>
<span data-ttu-id="33a35-138">인증서 서명 메서드에 대한 제한은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-138">There is no restriction on the certificate signature methods.</span></span> <span data-ttu-id="33a35-139">ECC(타원 곡선암호화), SAN(주체 대체 이름 ) 및 다른 일반적인 인증서 형식은 모두 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-139">Elliptic Curve Cryptography (ECC), Subject Alternative Name (SAN), and other common certificate types are all supported.</span></span> 

<span data-ttu-id="33a35-140">와일드카드가 원하는 외부 URL과 일치하는 한 와일드카드 인증서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-140">You can use a wildcard certificate as long as the wildcard matches the desired external URL.</span></span> 

<span data-ttu-id="33a35-141">자체 서명된 인증서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-141">You can use self-signed certificates, as well.</span></span> <span data-ttu-id="33a35-142">개인 인증 기관을 사용하는 경우 인증서에 대한 CDP(인증서 해지 지점 배포 지점)는 공용이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-142">If you’re using a private certificate authority, the CDP (certificate revocation point distribution point) for the certificate should be public.</span></span>

### <a name="changing-the-domain"></a><span data-ttu-id="33a35-143">도메인 변경</span><span class="sxs-lookup"><span data-stu-id="33a35-143">Changing the domain</span></span>
<span data-ttu-id="33a35-144">모든 확인된 도메인은 응용 프로그램에 대한 외부 URL 드롭다운 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-144">All verified domains appear in the External URL dropdown list for your application.</span></span> <span data-ttu-id="33a35-145">도메인을 변경하려면 응용 프로그램에 대한 해당 필드를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-145">To change the domain, just update that field for the application.</span></span> <span data-ttu-id="33a35-146">원하는 도메인이 목록에 없는 경우 [확인된 도메인으로 추가](active-directory-domains-add-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-146">If the domain you want isn't in the list, [add it as a verified domain](active-directory-domains-add-azure-portal.md).</span></span> <span data-ttu-id="33a35-147">연결된 인증서가 없는 도메인을 선택하는 경우 5-7단계를 수행하여 인증서를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-147">If you select a domain that doesn't have an associated certificate yet, follow steps 5-7 to add the certificate.</span></span> <span data-ttu-id="33a35-148">그런 다음 새 외부 URL에서 리디렉션할 DNS 레코드를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-148">Then, make sure you update the DNS record to redirect from the new external URL.</span></span> 

### <a name="certificate-management"></a><span data-ttu-id="33a35-149">인증서 관리</span><span class="sxs-lookup"><span data-stu-id="33a35-149">Certificate management</span></span>
<span data-ttu-id="33a35-150">응용 프로그램이 외부 호스트를 공유하지 않는 한 여러 응용 프로그램에 대해 동일한 인증서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-150">You can use the same certificate for multiple applications unless the applications share an external host.</span></span> 

<span data-ttu-id="33a35-151">인증서가 만료되면 포털을 통해 다른 인증서를 업로드하라는 경고를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-151">You get a warning when a certificate expires, telling you to upload another certificate through the portal.</span></span> <span data-ttu-id="33a35-152">인증서가 해지되면 응용 프로그램에 액세스할 때 보안 경고를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-152">If the certificate is revoked, your users may see a security warning when accessing the application.</span></span> <span data-ttu-id="33a35-153">인증서에 대한 해지 검사를 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-153">We don’t perform revocation checks for certificates.</span></span>  <span data-ttu-id="33a35-154">지정된 응용 프로그램에 대한 인증서를 업데이트하려면 응용 프로그램으로 이동하고 게시된 응용 프로그램에 사용자 지정 도메인 구성에 대한 5-7단계를 수행하여 새 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-154">To update the certificate for a given application, navigate to the application and follow steps 5-7 for configuring custom domains on published applications to upload a new certificate.</span></span> <span data-ttu-id="33a35-155">이전 인증서가 다른 응용 프로그램에서 사용되고 있지 않으면 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-155">If the old certificate is not being used by other applications, it is deleted automatically.</span></span> 

<span data-ttu-id="33a35-156">현재 모든 인증서 관리는 개별 응용 프로그램 페이지를 통하므로 관련 응용 프로그램의 컨텍스트에서 인증서를 관리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33a35-156">Currently all certificate management is through individual application pages so you need to manage certificates in the context of the relevant applications.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="33a35-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="33a35-157">Next steps</span></span>
* <span data-ttu-id="33a35-158">Azure AD 인증을 사용하여 게시된 앱에 대해 [Single Sign-On 사용](active-directory-application-proxy-sso-using-kcd.md)</span><span class="sxs-lookup"><span data-stu-id="33a35-158">[Enable single sign-on](active-directory-application-proxy-sso-using-kcd.md) to your published apps with Azure AD authentication.</span></span>
* <span data-ttu-id="33a35-159">게시된 앱에 대해 [조건부 액세스 사용](active-directory-application-proxy-conditional-access.md)</span><span class="sxs-lookup"><span data-stu-id="33a35-159">[Enable conditional access](active-directory-application-proxy-conditional-access.md) to your published apps.</span></span>
* [<span data-ttu-id="33a35-160">Azure AD에 사용자 지정 도메인 이름 추가</span><span class="sxs-lookup"><span data-stu-id="33a35-160">Add your custom domain name to Azure AD</span></span>](active-directory-domains-add-azure-portal.md)


