---
title: "Azure Active Directory B2C: Facebook 구성 | Microsoft Docs"
description: "소비자에게 Azure Active Directory B2C를 사용하여 보안이 유지되는 응용 프로그램에서 Facebook 계정으로 등록 및 로그인 제공"
services: active-directory-b2c
documentationcenter: 
author: sromeroz
manager: krassk
editor: sromeroz
ms.assetid: b875f235-a1d2-4abb-b9f0-b89beac38a32
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/7/2017
ms.author: sromeroz
ms.openlocfilehash: 8c2154fcf33537358b549395d15b4ba937371cd0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-facebook-accounts"></a><span data-ttu-id="83c19-103">Azure Active Directory B2C: 고객에게 Facebook 계정으로 등록 및 로그인 제공</span><span class="sxs-lookup"><span data-stu-id="83c19-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Facebook accounts</span></span>
## <a name="create-a-facebook-application"></a><span data-ttu-id="83c19-104">Facebook 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="83c19-104">Create a Facebook application</span></span>
<span data-ttu-id="83c19-105">Azure Active Directory(Azure AD) B2C에서 Facebook을 ID 공급자로 사용하려면 Facebook 응용 프로그램을 만들고 올바른 매개 변수를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-105">To use Facebook as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Facebook application and supply it with the right parameters.</span></span> <span data-ttu-id="83c19-106">이 작업을 수행하려면 Facebook 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-106">You need a Facebook account to do this.</span></span> <span data-ttu-id="83c19-107">계정이 없는 경우 [https://www.facebook.com/](https://www.facebook.com/)에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-107">If you don’t have one, you can get it at [https://www.facebook.com/](https://www.facebook.com/).</span></span>

1. <span data-ttu-id="83c19-108">[Facebook 개발자 웹 사이트](https://developers.facebook.com/) 로 이동한 다음 Facebook 계정 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-108">Go to the [Facebook for developers](https://developers.facebook.com/) website and sign in with your Facebook account credentials.</span></span>
2. <span data-ttu-id="83c19-109">아직 등록하지 않은 경우 Facebook 개발자로 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-109">If you have not already done so, you need to register as a Facebook developer.</span></span> <span data-ttu-id="83c19-110">등록하려면 페이지의 오른쪽 위에서 **등록**을 클릭하고 Facebook의 정책에 동의하고 등록 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-110">To do this, click **Register** (on the upper-right corner of the page), accept Facebook's policies, and complete the registration steps.</span></span>
3. <span data-ttu-id="83c19-111">**내 앱**을 클릭한 후 **새 앱 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-111">Click **My Apps** and then click **Add a New App**.</span></span> 
4. <span data-ttu-id="83c19-112">형식에서 **표시 이름** 및 유효한 **연락처 전자 메일**을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-112">In the form, provide a **Display Name** and a valid **Contact Email**.</span></span>
5. <span data-ttu-id="83c19-113">**앱 ID 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-113">Click **Create App ID**.</span></span> <span data-ttu-id="83c19-114">Facebook 플랫폼 정책을 수용하고 온라인 보안 검사를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-114">This may require you to accept Facebook platform policies and complete an online security check.</span></span>
6. <span data-ttu-id="83c19-115">왼쪽 열에서 **설정**을 클릭한 다음 아직 선택하지 않은 경우 **기본**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-115">In the left column, click **Settings** and then select **Basic** if not selected already.</span></span>
7. <span data-ttu-id="83c19-116">**범주**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-116">Select a **Category**.</span></span> 
8. <span data-ttu-id="83c19-117">**+플랫폼 추가**를 클릭하고 **웹 사이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-117">Click **+ Add Platform** and select **Website**.</span></span>
   
    ![Facebook - 설정](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook - 설정 - 웹 사이트](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. <span data-ttu-id="83c19-120">**사이트 URL** 필드에 `https://login.microsoftonline.com/`을 입력한 다음 페이지의 맨 아래에서 **변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-120">Enter `https://login.microsoftonline.com/` in the **Site URL** field and then click **Save Changes** at the bottom of the page.</span></span>
   
    ![Facebook - 사이트 URL](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. <span data-ttu-id="83c19-122">**앱 ID**의 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-122">Copy the value of **App ID**.</span></span> <span data-ttu-id="83c19-123">**표시**를 클릭하고 **앱 비밀** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-123">Click **Show** and copy the value of **App Secret**.</span></span> <span data-ttu-id="83c19-124">테넌트에서 Facebook을 ID 공급자로 구성하려면 둘 다 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-124">You will need both of them to configure Facebook as an identity provider in your tenant.</span></span> <span data-ttu-id="83c19-125">**앱 암호** 는 중요한 보안 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-125">**App Secret** is an important security credential.</span></span>
   
    ![Facebook - 앱 ID 및 앱 암호](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. <span data-ttu-id="83c19-127">왼쪽 탐색 영역에서 **+ 제품 추가**를 클릭하고 **Facebook 로그인**에 대한 **설정** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-127">Click **+ Add Product** on the left navigation and then the **Set Up** button for **Facebook Login**.</span></span>
   
    ![Facebook - Facebook 로그인](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. <span data-ttu-id="83c19-129">**Facebook 로그인** 아래의 오른쪽 탐색 영역에서 **설정** 클릭</span><span class="sxs-lookup"><span data-stu-id="83c19-129">Click **Settings** on the right nav under **Facebook Login**</span></span>

    ![Facebook - Facebook 로그인 설정](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. <span data-ttu-id="83c19-131">**클라이언트 OAuth 설정** 섹션의 **유효한 OAuth 리디렉션 URI** 필드에 `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-131">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Valid OAuth redirect URIs** field in the **Client OAuth Settings** section.</span></span> <span data-ttu-id="83c19-132">**{tenant}** 를 사용자의 테넌트 이름(예: contosob2c.onmicrosoft.com)으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-132">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="83c19-133">페이지 아래쪽에 있는 **변경 내용 저장** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-133">Click **Save Changes** at the bottom of the page.</span></span>
    
    ![Facebook - OAuth 리디렉션 URI](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. <span data-ttu-id="83c19-135">Facebook 응용 프로그램을 Azure AD B2C에서 사용할 수 있도록 하려면 공개적으로 사용할 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-135">To make your Facebook application usable by Azure AD B2C, you need to make it publicly available.</span></span> <span data-ttu-id="83c19-136">이렇게 하려면 왼쪽 탐색 창에서 **앱 검토**를 클릭하고 페이지의 위쪽에 있는 스위치를 **예**로 설정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-136">You can do this by clicking **App Review** on the left navigation and by turning the switch at the top of the page to **YES** and clicking **Confirm**.</span></span>
    
    ![Facebook - 앱 공개](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="83c19-138">테넌트에서 Facebook을 ID 공급자로 구성</span><span class="sxs-lookup"><span data-stu-id="83c19-138">Configure Facebook as an identity provider in your tenant</span></span>
1. <span data-ttu-id="83c19-139">다음 단계에 따라 [Azure Portal의 B2C 기능 블레이드로 이동합니다](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) .</span><span class="sxs-lookup"><span data-stu-id="83c19-139">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="83c19-140">B2C 기능 블레이드에서 **ID 공급자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-140">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="83c19-141">블레이드의 위쪽에서 **+추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-141">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="83c19-142">ID 공급자 구성에 친숙한 **이름** 을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-142">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="83c19-143">예를 들어 "Facebook"을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-143">For example, enter "Facebook".</span></span>
5. <span data-ttu-id="83c19-144">**ID 공급자 형식**을 클릭하고 **Facebook**을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-144">Click **Identity provider type**, select **Facebook**, and click **OK**.</span></span>
6. <span data-ttu-id="83c19-145">**이 ID 공급자 설정**을 클릭하고 이전에 만든 Facebook 응용 프로그램의 앱 ID 및 앱 비밀을 **클라이언트 ID** 및 **클라이언트 비밀** 필드에 각각 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-145">Click **Set up this identity provider** and enter the app ID and app secret (of the Facebook application that you created earlier) in the **Client ID** and **Client secret** fields respectively.</span></span>
7. <span data-ttu-id="83c19-146">**확인**, **만들기**를 차례로 클릭하여 Facebook 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-146">Click **OK**, and then click **Create** to save your Facebook configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="83c19-147">테넌트에 **ID 공급자**를 추가해도 기존 정책이 수정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-147">Adding an **Identity provider** to your tenant does not modify your existing policies.</span></span> <span data-ttu-id="83c19-148">방금 만든 ID 공급자를 포함하여 정책을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83c19-148">Remember to update your policies by including the identity provider you just created.</span></span>
>