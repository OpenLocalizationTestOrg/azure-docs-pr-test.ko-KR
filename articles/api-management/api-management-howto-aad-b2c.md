---
title: "Azure Active Directory B2C를 사용하여 개발자 계정에 권한 부여 - Azure API Management | Microsoft Docs"
description: "API Management에서 Azure Active Directory B2C를 사용하여 사용자에게 권한을 부여하는 방법에 대해 알아보세요."
services: api-management
documentationcenter: API Management
author: miaojiang
manager: erikre
editor: 
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: eb7deb1a79d9db9ac5cfbea69b8d3c564eb55577
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-authorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a><span data-ttu-id="63052-103">Azure API Management에서 Azure Active Directory B2C를 사용하여 개발자 계정에 권한을 부여하는 방법</span><span class="sxs-lookup"><span data-stu-id="63052-103">How to authorize developer accounts by using Azure Active Directory B2C in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="63052-104">개요</span><span class="sxs-lookup"><span data-stu-id="63052-104">Overview</span></span>
<span data-ttu-id="63052-105">Azure Active Directory B2C는 소비자 지향 웹 및 모바일 응용 프로그램을 위한 클라우드 ID 관리 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="63052-105">Azure Active Directory B2C is a cloud identity management solution for consumer-facing web and mobile applications.</span></span> <span data-ttu-id="63052-106">개발자 포털에 대한 액세스 권한을 관리하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63052-106">You can use it to manage access to your developer portal.</span></span> <span data-ttu-id="63052-107">이 가이드에서는 Azure Active Directory B2C와 통합하려는 API Management 서비스에 필요한 구성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="63052-107">This guide shows you the configuration that's required in your API Management service to integrate with Azure Active Directory B2C.</span></span> <span data-ttu-id="63052-108">클래식 Azure Active Directory를 사용하여 개발자 포털에 대한 액세스를 사용하는 방법에 대한 정보는 [Azure Active Directory를 사용하여 개발자 계정에 권한을 부여하는 방법]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63052-108">For information about enabling access to the developer portal by using classic Azure Active Directory, see [How to authorize developer accounts using Azure Active Directory].</span></span>

> [!NOTE]
> <span data-ttu-id="63052-109">이 가이드의 단계를 완료하려면 먼저 응용 프로그램을 만들 Azure Active Directory B2C 테넌트가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63052-109">To complete the steps in this guide, you must first have an Azure Active Directory B2C tenant to create an application in.</span></span> <span data-ttu-id="63052-110">또한, 등록 및 로그인 정책이 준비되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63052-110">Also, you need to have signup and signin policies ready.</span></span> <span data-ttu-id="63052-111">자세한 내용은 [Azure Active Directory B2C 개요]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63052-111">For more information, see [Azure Active Directory B2C overview].</span></span>

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a><span data-ttu-id="63052-112">Azure Active Directory B2C를 사용하여 개발자 계정에 권한 부여</span><span class="sxs-lookup"><span data-stu-id="63052-112">Authorize developer accounts by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="63052-113">시작하려면 Azure Portal에서 API Management 서비스에 대한 **게시자 포털**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63052-113">To get started, click **Publisher portal** in the Azure portal for your API Management service.</span></span> <span data-ttu-id="63052-114">API 관리 게시자 포털로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="63052-114">This takes you to the API Management publisher portal.</span></span>

   ![게시자 포털][api-management-management-console]

   > [!NOTE]
   > <span data-ttu-id="63052-116">아직 API Management 서비스 인스턴스를 만들지 않은 경우 [Azure API Management 시작 자습서][Get started with Azure API Management]의 [API Management 서비스 인스턴스 만들기][Create an API Management service instance]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63052-116">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management tutorial][Get started with Azure API Management].</span></span>

2. <span data-ttu-id="63052-117">**API Management** 메뉴에서 **보안**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63052-117">On the **API Management** menu, click **Security**.</span></span> <span data-ttu-id="63052-118">**ID** 탭에서 **Azure Active Directory B2C**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="63052-118">On the **Identities** tab, choose **Azure Active Directory B2C**.</span></span>

  ![외부 ID 1][api-management-howto-aad-b2c-security-tab]

3. <span data-ttu-id="63052-120">**리디렉션 URL**을 기록해 두고 Azure Portal에서 Azure Active Directory B2C로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="63052-120">Make a note of the **Redirect URL** and switch over to Azure Active Directory B2C in the Azure portal.</span></span>

  ![외부 ID 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. <span data-ttu-id="63052-122">**응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63052-122">Click the **Applications** button.</span></span>

  ![새 응용 프로그램 1 등록][api-management-howto-aad-b2c-portal-menu]

5. <span data-ttu-id="63052-124">**추가** 단추를 클릭하여 새 Azure Active Directory B2C 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="63052-124">Click the **Add** button to create a new Azure Active Directory B2C application.</span></span>

  ![새 응용 프로그램 2 등록][api-management-howto-aad-b2c-add-button]

6. <span data-ttu-id="63052-126">**새 응용 프로그램** 블레이드에서 응용 프로그램의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="63052-126">In the **New application** blade, enter a name for the application.</span></span> <span data-ttu-id="63052-127">**Web App/Web API**에서 **예**를 선택하고 **암시적 흐름 허용**에서 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="63052-127">Choose **Yes** under **Web App/Web API**, and choose **Yes** under **Allow implicit flow**.</span></span> <span data-ttu-id="63052-128">그런 다음, 게시자 포털의 **ID** 탭에 있는 **Azure Active Directory B2C** 섹션에서 **리디렉션 URL**을 복사하여 **회신 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="63052-128">Then copy the **Redirect URL** from the **Azure Active Directory B2C** section of the **Identities** tab in the publisher portal, and paste it into the **Reply URL** text box.</span></span>

  ![새 응용 프로그램 3 등록][api-management-howto-aad-b2c-app-details]

7. <span data-ttu-id="63052-130">**만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63052-130">Click the **Create** button.</span></span> <span data-ttu-id="63052-131">응용 프로그램이 만들어지면 **응용 프로그램** 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="63052-131">When the application is created, it appears in the **Applications** blade.</span></span> <span data-ttu-id="63052-132">세부 정보를 보려면 응용 프로그램 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63052-132">Click the application name to see its details.</span></span>

  ![새 응용 프로그램 4 등록][api-management-howto-aad-b2c-app-created]

8. <span data-ttu-id="63052-134">**속성** 블레이드에서 **응용 프로그램 ID**를 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="63052-134">From the **Properties** blade, copy the **Application ID** to the clipboard.</span></span>

  ![응용 프로그램 ID 1][api-management-howto-aad-b2c-app-id]

9. <span data-ttu-id="63052-136">게시자 포털로 다시 전환하고 ID를 **클라이언트 ID** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="63052-136">Switch back to the publisher portal and paste the ID into the **Client Id** text box.</span></span>

  ![응용 프로그램 ID 2][api-management-howto-aad-b2c-client-id]

10. <span data-ttu-id="63052-138">Azure Portal로 다시 전환하고 **키** 단추를 클릭한 다음 **키 생성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63052-138">Switch back to the Azure portal, click the **Keys** button, and then click **Generate key**.</span></span> <span data-ttu-id="63052-139">**저장**을 클릭하여 구성을 저장하고 **앱 키**를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="63052-139">Click **Save** to save the configuration and display the **App key**.</span></span> <span data-ttu-id="63052-140">키를 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="63052-140">Copy the key to the clipboard.</span></span>

  ![앱 키 1][api-management-howto-aad-b2c-app-key]

11. <span data-ttu-id="63052-142">게시자 포털로 다시 전환하고 키를 **클라이언트 암호** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="63052-142">Switch back to the publisher portal and paste the key into the **Client Secret** text box.</span></span>

  ![앱 키 2][api-management-howto-aad-b2c-client-secret]

12. <span data-ttu-id="63052-144">**허용된 테넌트**에서 Azure Active Directory B2C 테넌트의 도메인 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="63052-144">Specify the domain name of the Azure Active Directory B2C tenant in **Allowed Tenant**.</span></span>

  ![허용된 테넌트][api-management-howto-aad-b2c-allowed-tenant]

13. <span data-ttu-id="63052-146">**등록 정책** 및 **로그인 정책**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="63052-146">Specify the **Signup Policy** and **Signin Policy**.</span></span> <span data-ttu-id="63052-147">선택적으로 **프로필 편집 정책** 및 **암호 재설정 정책**을 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63052-147">Optionally, you can also provide the **Profile Editing Policy** and **Password Reset Policy**.</span></span>

  ![정책][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > <span data-ttu-id="63052-149">정책에 대한 자세한 내용은 [Azure Active Directory B2C: 확장할 수 있는 정책 프레임워크]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63052-149">For more information on policies, see [Azure Active Directory B2C: Extensible policy framework].</span></span>

14. <span data-ttu-id="63052-150">원하는 구성이 지정되면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63052-150">After you've specified the desired configuration, click **Save**.</span></span>

  <span data-ttu-id="63052-151">변경 내용이 저장되면 개발자는 Azure Active Directory B2C를 사용하여 새 계정을 만들고 개발자 포털에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63052-151">After the changes are saved, developers will be able to create new accounts and sign in to the developer portal by using Azure Active Directory B2C.</span></span>

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a><span data-ttu-id="63052-152">Azure Active Directory B2C를 사용하여 개발자 계정에 등록</span><span class="sxs-lookup"><span data-stu-id="63052-152">Sign up for a developer account by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="63052-153">Azure Active Directory B2C를 사용하여 개발자 계정에 등록하려면 새 브라우저 창을 열고 개발자 포털로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="63052-153">To sign up for a developer account by using Azure Active Directory B2C, open a new browser window and go to the developer portal.</span></span> <span data-ttu-id="63052-154">**등록** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63052-154">Click the **Sign up** button.</span></span>

   ![개발자 포털 1][api-management-howto-aad-b2c-dev-portal]

2. <span data-ttu-id="63052-156">**Azure Active Directory B2C**를 사용하여 등록하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="63052-156">Choose to sign up with **Azure Active Directory B2C**.</span></span>

   ![개발자 포털 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. <span data-ttu-id="63052-158">이전 섹션에서 구성하였던 등록 정책으로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="63052-158">You're redirected to the signup policy that you configured in the previous section.</span></span> <span data-ttu-id="63052-159">전자 메일 주소 또는 기존 소셜 계정 중 하나를 사용하여 등록하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="63052-159">Choose to sign up by using your email address or one of your existing social accounts.</span></span>

   > [!NOTE]
   > <span data-ttu-id="63052-160">Azure Active Directory B2C가 게시자 포털의 **ID** 탭에서 사용하도록 설정되는 유일한 옵션인 경우 등록 정책에 직접 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="63052-160">If Azure Active Directory B2C is the only option that's enabled on the **Identities** tab in the publisher portal, you'll be redirected to the signup policy directly.</span></span>

   ![개발자 포털][api-management-howto-aad-b2c-dev-portal-b2c-options]

   <span data-ttu-id="63052-162">등록이 완료되면 개발자 포털로 다시 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="63052-162">When the signup is complete, you're redirected back to the developer portal.</span></span> <span data-ttu-id="63052-163">이제 API Management 서비스 인스턴스에 대한 개발자 포털에 로그인됩니다.</span><span class="sxs-lookup"><span data-stu-id="63052-163">You're now signed in to the developer portal for your API Management service instance.</span></span>

    ![등록 완료][api-management-registration-complete]

## <a name="next-steps"></a><span data-ttu-id="63052-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="63052-165">Next steps</span></span>

*  <span data-ttu-id="63052-166">[Azure Active Directory B2C 개요]</span><span class="sxs-lookup"><span data-stu-id="63052-166">[Azure Active Directory B2C overview]</span></span>
*  <span data-ttu-id="63052-167">[Azure Active Directory B2C: 확장할 수 있는 정책 프레임워크]</span><span class="sxs-lookup"><span data-stu-id="63052-167">[Azure Active Directory B2C: Extensible policy framework]</span></span>
*  <span data-ttu-id="63052-168">[Azure Active Directory B2C에서 Microsoft 계정을 ID 공급자로 사용]</span><span class="sxs-lookup"><span data-stu-id="63052-168">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="63052-169">[Azure Active Directory B2C에서 Google 계정을 ID 공급자로 사용]</span><span class="sxs-lookup"><span data-stu-id="63052-169">[Use a Google account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="63052-170">[Azure Active Directory B2C에서 LinkedIn 계정을 ID 공급자로 사용]</span><span class="sxs-lookup"><span data-stu-id="63052-170">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="63052-171">[Azure Active Directory B2C에서 Facebook 계정을 ID 공급자로 사용]</span><span class="sxs-lookup"><span data-stu-id="63052-171">[Use a Facebook account as an identity provider in Azure Active Directory B2C]</span></span>




[api-management-howto-aad-b2c-security-tab]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab.PNG
[api-management-howto-aad-b2c-security-tab-reply-url]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab-reply-url.PNG
[api-management-howto-aad-b2c-portal-menu]: ./media/api-management-howto-aad-b2c/api-management-b2c-portal-menu.PNG
[api-management-howto-aad-b2c-add-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-add-button.PNG
[api-management-howto-aad-b2c-app-details]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-details.PNG
[api-management-howto-aad-b2c-app-created]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-created.PNG
[api-management-howto-aad-b2c-app-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-id.PNG
[api-management-howto-aad-b2c-client-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-id.PNG
[api-management-howto-aad-b2c-app-key]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key.PNG
[api-management-howto-aad-b2c-app-key-saved]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key-saved.PNG
[api-management-howto-aad-b2c-client-secret]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-secret.PNG
[api-management-howto-aad-b2c-allowed-tenant]: ./media/api-management-howto-aad-b2c/api-management-b2c-allowed-tenant.PNG
[api-management-howto-aad-b2c-policies]: ./media/api-management-howto-aad-b2c/api-management-b2c-policies.PNG
[api-management-howto-aad-b2c-dev-portal]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-button.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-options]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-options.PNG
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.PNG
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-b2c-security-tab.png
[api-management-security-aad-new]: ./media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: ./media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: ./media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: ./media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: ./media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: ./media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: ./media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: ./media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: ./media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: ./media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: ./media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: ./media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-permissions-form]: ./media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: ./media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: ./media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: ./media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: ./media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: ./media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: ./media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: ./media/api-management-howto-aad/api-management-edit-group.png

[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing the Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph
<span data-ttu-id="63052-172">[Azure Active Directory B2C 개요]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview</span><span class="sxs-lookup"><span data-stu-id="63052-172">[Azure Active Directory B2C overview]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview</span></span>
<span data-ttu-id="63052-173">[Azure Active Directory를 사용하여 개발자 계정에 권한을 부여하는 방법]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad</span><span class="sxs-lookup"><span data-stu-id="63052-173">[How to authorize developer accounts using Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad</span></span>
<span data-ttu-id="63052-174">[Azure Active Directory B2C: 확장할 수 있는 정책 프레임워크]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies</span><span class="sxs-lookup"><span data-stu-id="63052-174">[Azure Active Directory B2C: Extensible policy framework]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies</span></span>
<span data-ttu-id="63052-175">[Azure Active Directory B2C에서 Microsoft 계정을 ID 공급자로 사용]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app</span><span class="sxs-lookup"><span data-stu-id="63052-175">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app</span></span>
<span data-ttu-id="63052-176">[Azure Active Directory B2C에서 Google 계정을 ID 공급자로 사용]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app</span><span class="sxs-lookup"><span data-stu-id="63052-176">[Use a Google account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app</span></span>
<span data-ttu-id="63052-177">[Azure Active Directory B2C에서 Facebook 계정을 ID 공급자로 사용]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app</span><span class="sxs-lookup"><span data-stu-id="63052-177">[Use a Facebook account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app</span></span>
<span data-ttu-id="63052-178">[Azure Active Directory B2C에서 LinkedIn 계정을 ID 공급자로 사용]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app</span><span class="sxs-lookup"><span data-stu-id="63052-178">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app</span></span>

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

[Log in to the Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account
