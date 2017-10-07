---
title: "Azure AD 응용 프로그램 프록시에 aaaCustom 도메인 | Microsoft Docs"
description: "Hello 앱에 대 한 해당 hello URL은 동일한 사용자가 액세스 하는 것에 관계 없이 hello Azure AD 응용 프로그램 프록시에 사용자 지정 도메인을 관리 합니다."
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
ms.openlocfilehash: 7a433c411976077210a2435c3c087991c7430755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a><span data-ttu-id="8fd80-103">Azure AD 응용 프로그램 프록시에서 사용자 지정 도메인 작업</span><span class="sxs-lookup"><span data-stu-id="8fd80-103">Working with custom domains in Azure AD Application Proxy</span></span>

<span data-ttu-id="8fd80-104">Azure Active Directory 응용 프로그램 프록시를 통해 응용 프로그램을 게시 하면 원격으로 작업 하는 사용자가 toogo toowhen 프로그램에 대 한 외부 URL을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-104">When you publish an application through Azure Active Directory Application Proxy, you create an external URL for your users toogo toowhen they're working remotely.</span></span> <span data-ttu-id="8fd80-105">이 URL 가져옵니다 hello 기본 도메인 *yourtenant.msappproxy.net*합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-105">This URL gets hello default domain *yourtenant.msappproxy.net*.</span></span> <span data-ttu-id="8fd80-106">예를 들어 게시 한 경우 응용 프로그램 이라는 비용 및 테 넌 트, Contoso 라는 있으면 hello 외부 URL 합니다 https://expenses-contoso.msappproxy.net 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-106">For example, if you published an app named Expenses and your tenant is named Contoso, then hello external URL would be https://expenses-contoso.msappproxy.net.</span></span> <span data-ttu-id="8fd80-107">자신의 도메인 이름을 toouse을 원하는 경우 응용 프로그램에 대 한 사용자 지정 도메인을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-107">If you want toouse your own domain name, configure a custom domain for your application.</span></span> 

<span data-ttu-id="8fd80-108">언제나 가능한 응용 프로그램에 대한 사용자 지정 도메인을 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-108">We recommend that you set up custom domains for your applications whenever possible.</span></span> <span data-ttu-id="8fd80-109">사용자 지정 도메인의 hello 이점 중 일부는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-109">Some of hello benefits of custom domains include:</span></span>

- <span data-ttu-id="8fd80-110">사용자가 toohello 응용 프로그램을 가져올 수 내부 또는 외부 네트워크에서 근무 하는 동일한 URL을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-110">Your users can get toohello application with hello same URL, whether they are working inside or outside of your network.</span></span>
- <span data-ttu-id="8fd80-111">동일한 내부 및 외부 Url hello는의 모든 응용 프로그램, tooanother 가리키는 한 응용 프로그램에서 링크 hello 회사 네트워크 외부 에서도 toowork를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-111">If all of your applications have hello same internal and external URLs, then links in one application that point tooanother continue toowork even outside hello corporate network.</span></span> 
- <span data-ttu-id="8fd80-112">브랜딩, 제어 및 원하는 hello Url을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-112">You control your branding, and create hello URLs you want.</span></span> 


## <a name="configure-a-custom-domain"></a><span data-ttu-id="8fd80-113">사용자 지정 도메인 구성</span><span class="sxs-lookup"><span data-stu-id="8fd80-113">Configure a custom domain</span></span>

### <a name="prerequisites"></a><span data-ttu-id="8fd80-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8fd80-114">Prerequisites</span></span>

<span data-ttu-id="8fd80-115">사용자 지정 도메인을 구성 하기 전에 hello 준비 하는 요구 사항을 준수 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-115">Before you configure a custom domain, make sure that you have hello following requirements prepared:</span></span> 
- <span data-ttu-id="8fd80-116">A [확인 된 도메인이 추가 Active Directory tooAzure](active-directory-domains-add-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-116">A [verified domain added tooAzure Active Directory](active-directory-domains-add-azure-portal.md).</span></span>
- <span data-ttu-id="8fd80-117">PFX 파일의 hello 형태로 hello 도메인에 대 한 사용자 지정 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-117">A custom certificate for hello domain, in hello form of a PFX file.</span></span> 
- <span data-ttu-id="8fd80-118">[응용 프로그램 프록시를 통해 게시된](application-proxy-publish-azure-portal.md) 온-프레미스 앱.</span><span class="sxs-lookup"><span data-stu-id="8fd80-118">An on-premises app [published through Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

### <a name="configure-your-custom-domain"></a><span data-ttu-id="8fd80-119">사용자 지정 도메인 구성</span><span class="sxs-lookup"><span data-stu-id="8fd80-119">Configure your custom domain</span></span>

<span data-ttu-id="8fd80-120">이러한 세 가지 요구 사항을 준비 해야 하는 경우 이러한 단계 tooset을 사용자 지정 도메인을 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="8fd80-120">When you have those three requirements ready, follow these steps tooset up your custom domain:</span></span>

1. <span data-ttu-id="8fd80-121">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-121">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8fd80-122">너무 이동**Azure Active Directory** > **엔터프라이즈 응용 프로그램** > **모든 응용 프로그램** hello 응용 프로그램을 선택 하 고 원하는 toomanage 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-122">Navigate too**Azure Active Directory** > **Enterprise applications** > **All applications** and choose hello app you want toomanage.</span></span>
3. <span data-ttu-id="8fd80-123">**응용 프로그램 프록시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-123">Select **Application Proxy**.</span></span> 
4. <span data-ttu-id="8fd80-124">Hello 외부 URL 필드에 hello 드롭다운 목록 tooselect 사용자 지정 도메인을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-124">In hello External URL field, use hello dropdown list tooselect your custom domain.</span></span> <span data-ttu-id="8fd80-125">Hello 목록에서 도메인을 보이지 않으면 다음 그 아직 확인 되지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-125">If you don't see your domain in hello list, then it hasn't been verified yet.</span></span> 
5. <span data-ttu-id="8fd80-126">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-126">Select **Save**</span></span>
5. <span data-ttu-id="8fd80-127">hello **인증서** 사용할 수 없는 필드에 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-127">hello **Certificate** field that was disabled becomes enabled.</span></span> <span data-ttu-id="8fd80-128">이 필드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-128">Select this field.</span></span> 

   ![Tooupload 인증서를 클릭 합니다.](./media/active-directory-application-proxy-custom-domains/certificate.png)

   <span data-ttu-id="8fd80-130">아직이 도메인에 대 한 인증서를 업로드 하는 경우 hello 인증서 필드 hello 인증서 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-130">If you already uploaded a certificate for this domain, hello Certificate field displays hello certificate information.</span></span> 

6. <span data-ttu-id="8fd80-131">Hello PFX 인증서를 업로드 하 고 hello 인증서에 대 한 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-131">Upload hello PFX certificate and enter hello password for hello certificate.</span></span> 
7. <span data-ttu-id="8fd80-132">선택 **저장** toosave 변경 내용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-132">Select **Save** toosave your changes.</span></span> 
8. <span data-ttu-id="8fd80-133">추가 [DNS 레코드](../dns/dns-operations-recordsets-portal.md) 리디렉션을 새 외부 URL toohello msappproxy.net 도메인 hello 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-133">Add a [DNS record](../dns/dns-operations-recordsets-portal.md) that redirects hello new external URL toohello msappproxy.net domain.</span></span> 

>[!TIP] 
><span data-ttu-id="8fd80-134">사용자 지정 도메인당 하나의 인증서 tooupload 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-134">You only need tooupload one certificate per custom domain.</span></span> <span data-ttu-id="8fd80-135">인증서를 업로드 한 후 새 응용 프로그램을 게시 하 고 hello DNS 레코드를 제외 하 고 추가 구성이 toodo hello 사용자 지정 도메인을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-135">Once you upload a certificate, you can choose hello custom domain when you publish a new app and not have toodo additional configuration except for hello DNS record.</span></span> 

## <a name="manage-certificates"></a><span data-ttu-id="8fd80-136">인증서 관리</span><span class="sxs-lookup"><span data-stu-id="8fd80-136">Manage certificates</span></span>

### <a name="certificate-format"></a><span data-ttu-id="8fd80-137">인증서 형식</span><span class="sxs-lookup"><span data-stu-id="8fd80-137">Certificate format</span></span>
<span data-ttu-id="8fd80-138">Hello 인증서 서명 방법에 대 한 제한은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-138">There is no restriction on hello certificate signature methods.</span></span> <span data-ttu-id="8fd80-139">ECC(타원 곡선암호화), SAN(주체 대체 이름 ) 및 다른 일반적인 인증서 형식은 모두 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-139">Elliptic Curve Cryptography (ECC), Subject Alternative Name (SAN), and other common certificate types are all supported.</span></span> 

<span data-ttu-id="8fd80-140">Hello 와일드 카드 원하는 hello 외부 URL과 일치으로 와일드 카드 인증서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-140">You can use a wildcard certificate as long as hello wildcard matches hello desired external URL.</span></span> 

<span data-ttu-id="8fd80-141">자체 서명된 인증서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-141">You can use self-signed certificates, as well.</span></span> <span data-ttu-id="8fd80-142">개인 인증 기관을 사용 하는 hello CDP (인증서 해지 지점 배포 지점) hello 인증서에 대 한 공용 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-142">If you’re using a private certificate authority, hello CDP (certificate revocation point distribution point) for hello certificate should be public.</span></span>

### <a name="changing-hello-domain"></a><span data-ttu-id="8fd80-143">Hello 도메인 변경</span><span class="sxs-lookup"><span data-stu-id="8fd80-143">Changing hello domain</span></span>
<span data-ttu-id="8fd80-144">모든 확인 된 도메인 응용 프로그램에 대 한 hello 외부 URL 드롭다운 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-144">All verified domains appear in hello External URL dropdown list for your application.</span></span> <span data-ttu-id="8fd80-145">toochange hello 도메인, hello 응용 프로그램에 대 한 필드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-145">toochange hello domain, just update that field for hello application.</span></span> <span data-ttu-id="8fd80-146">Hello 도메인 hello 목록에 없으면 [확인 된 도메인으로 추가](active-directory-domains-add-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-146">If hello domain you want isn't in hello list, [add it as a verified domain](active-directory-domains-add-azure-portal.md).</span></span> <span data-ttu-id="8fd80-147">에 연결 된 인증서가 아직 없는 도메인을 선택 하는 경우 tooadd hello 인증서를 5-7 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-147">If you select a domain that doesn't have an associated certificate yet, follow steps 5-7 tooadd hello certificate.</span></span> <span data-ttu-id="8fd80-148">그런 다음 hello 새 외부 URL에서 DNS 레코드 tooredirect hello를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-148">Then, make sure you update hello DNS record tooredirect from hello new external URL.</span></span> 

### <a name="certificate-management"></a><span data-ttu-id="8fd80-149">인증서 관리</span><span class="sxs-lookup"><span data-stu-id="8fd80-149">Certificate management</span></span>
<span data-ttu-id="8fd80-150">Hello hello 응용 프로그램 외부 호스트를 공유 하지 않는 한 여러 응용 프로그램에 대 한 동일한 인증서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-150">You can use hello same certificate for multiple applications unless hello applications share an external host.</span></span> 

<span data-ttu-id="8fd80-151">경고가 나타나면 인증서가 만료 되 면 tooupload 알리는 hello 포털을 통해 다른 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-151">You get a warning when a certificate expires, telling you tooupload another certificate through hello portal.</span></span> <span data-ttu-id="8fd80-152">Hello 인증서가 해지 되는 경우 hello 응용 프로그램에 액세스할 때 보안 경고를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-152">If hello certificate is revoked, your users may see a security warning when accessing hello application.</span></span> <span data-ttu-id="8fd80-153">인증서에 대한 해지 검사를 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-153">We don’t perform revocation checks for certificates.</span></span>  <span data-ttu-id="8fd80-154">지정된 된 응용 프로그램에 대 한 tooupdate hello 인증서 toohello 응용 프로그램을 탐색 하 고 게시 된 응용 프로그램 tooupload 새 인증서에 사용자 지정 도메인 구성에 대 한 5-7 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-154">tooupdate hello certificate for a given application, navigate toohello application and follow steps 5-7 for configuring custom domains on published applications tooupload a new certificate.</span></span> <span data-ttu-id="8fd80-155">Hello 이전 인증서는 다른 응용 프로그램에서 사용 되 고 하지 않으면, 자동으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-155">If hello old certificate is not being used by other applications, it is deleted automatically.</span></span> 

<span data-ttu-id="8fd80-156">현재 모든 인증서 관리 이므로 개별 응용 프로그램 페이지를 통해 hello 관련 응용 프로그램의 hello 컨텍스트에서 toomanage 인증서가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-156">Currently all certificate management is through individual application pages so you need toomanage certificates in hello context of hello relevant applications.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8fd80-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8fd80-157">Next steps</span></span>
* <span data-ttu-id="8fd80-158">[Single sign-on 사용](active-directory-application-proxy-sso-using-kcd.md) tooyour Azure AD 인증을 사용 하 여 앱을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-158">[Enable single sign-on](active-directory-application-proxy-sso-using-kcd.md) tooyour published apps with Azure AD authentication.</span></span>
* <span data-ttu-id="8fd80-159">[조건부 액세스를 사용](active-directory-application-proxy-conditional-access.md) tooyour 게시 된 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="8fd80-159">[Enable conditional access](active-directory-application-proxy-conditional-access.md) tooyour published apps.</span></span>
* [<span data-ttu-id="8fd80-160">사용자 지정 도메인 이름을 tooAzure AD 추가</span><span class="sxs-lookup"><span data-stu-id="8fd80-160">Add your custom domain name tooAzure AD</span></span>](active-directory-domains-add-azure-portal.md)


