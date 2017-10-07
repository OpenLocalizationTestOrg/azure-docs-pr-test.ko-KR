---
title: "Azure Active Directory B2C: Facebook 구성 | Microsoft Docs"
description: "Azure Active Directory B2C에 의해 보안 되는 응용 프로그램에서 Facebook 계정에 등록 및 로그인 tooconsumers를 제공 합니다."
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
ms.openlocfilehash: 4c3b79c7248bd1e789bf33fc467abb27d0170edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-facebook-accounts"></a><span data-ttu-id="0afe9-103">Azure Active Directory B2C: Facebook 계정 등록 및 로그인 tooconsumers 제공</span><span class="sxs-lookup"><span data-stu-id="0afe9-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Facebook accounts</span></span>
## <a name="create-a-facebook-application"></a><span data-ttu-id="0afe9-104">Facebook 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="0afe9-104">Create a Facebook application</span></span>
<span data-ttu-id="0afe9-105">Facebook toouse (Azure AD) Azure Active Directory B2C에을 id 공급자로 Facebook 응용 프로그램 toocreate 필요 하 고이 hello 오른쪽 매개 변수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-105">toouse Facebook as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Facebook application and supply it with hello right parameters.</span></span> <span data-ttu-id="0afe9-106">사용자는 Facebook 계정 toodo이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-106">You need a Facebook account toodo this.</span></span> <span data-ttu-id="0afe9-107">계정이 없는 경우 [https://www.facebook.com/](https://www.facebook.com/)에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-107">If you don’t have one, you can get it at [https://www.facebook.com/](https://www.facebook.com/).</span></span>

1. <span data-ttu-id="0afe9-108">Toohello 이동 [개발자를 위한 Facebook](https://developers.facebook.com/) 계정 자격 증명을 웹 사이트 및 사용자가 Facebook으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-108">Go toohello [Facebook for developers](https://developers.facebook.com/) website and sign in with your Facebook account credentials.</span></span>
2. <span data-ttu-id="0afe9-109">아직 수행 경우 Facebook 개발자 tooregister가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-109">If you have not already done so, you need tooregister as a Facebook developer.</span></span> <span data-ttu-id="0afe9-110">toodo이를 클릭 하이 여 **등록** (hello 오른쪽 위 모서리에 hello 페이지의), Facebook의 정책 수락한 hello 등록 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-110">toodo this, click **Register** (on hello upper-right corner of hello page), accept Facebook's policies, and complete hello registration steps.</span></span>
3. <span data-ttu-id="0afe9-111">**내 앱**을 클릭한 후 **새 앱 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-111">Click **My Apps** and then click **Add a New App**.</span></span> 
4. <span data-ttu-id="0afe9-112">Hello 형태로 제공는 **표시 이름** 있고 유효한 **Contact Email**합니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-112">In hello form, provide a **Display Name** and a valid **Contact Email**.</span></span>
5. <span data-ttu-id="0afe9-113">**앱 ID 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-113">Click **Create App ID**.</span></span> <span data-ttu-id="0afe9-114">Tooaccept Facebook 플랫폼 정책을 요구 하 고 온라인 보안 검사를 완료할 수 있습니다이 합니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-114">This may require you tooaccept Facebook platform policies and complete an online security check.</span></span>
6. <span data-ttu-id="0afe9-115">Hello 왼쪽된 열에서 클릭 **설정** 선택한 후 **기본** 이미 선택 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-115">In hello left column, click **Settings** and then select **Basic** if not selected already.</span></span>
7. <span data-ttu-id="0afe9-116">**범주**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-116">Select a **Category**.</span></span> 
8. <span data-ttu-id="0afe9-117">**+플랫폼 추가**를 클릭하고 **웹 사이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-117">Click **+ Add Platform** and select **Website**.</span></span>
   
    ![Facebook - 설정](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook - 설정 - 웹 사이트](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. <span data-ttu-id="0afe9-120">입력 `https://login.microsoftonline.com/` hello에 **사이트 URL** 필드를 클릭 한 다음 **변경 내용 저장** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-120">Enter `https://login.microsoftonline.com/` in hello **Site URL** field and then click **Save Changes** at hello bottom of hello page.</span></span>
   
    ![Facebook - 사이트 URL](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. <span data-ttu-id="0afe9-122">hello 값을 복사 **앱 ID**합니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-122">Copy hello value of **App ID**.</span></span> <span data-ttu-id="0afe9-123">클릭 **표시** 의 hello 값을 복사 하 고 **응용 프로그램 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-123">Click **Show** and copy hello value of **App Secret**.</span></span> <span data-ttu-id="0afe9-124">둘 모두 필요 합니다 tooconfigure Facebook id 공급자로 테 넌 트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-124">You will need both of them tooconfigure Facebook as an identity provider in your tenant.</span></span> <span data-ttu-id="0afe9-125">**앱 암호** 는 중요한 보안 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-125">**App Secret** is an important security credential.</span></span>
   
    ![Facebook - 앱 ID 및 앱 암호](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. <span data-ttu-id="0afe9-127">클릭 **제품 추가 +** 왼쪽된 탐색 hello 되 고 다음 hello **Set Up** 단추에 대 한 **Facebook 로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-127">Click **+ Add Product** on hello left navigation and then hello **Set Up** button for **Facebook Login**.</span></span>
   
    ![Facebook - Facebook 로그인](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. <span data-ttu-id="0afe9-129">클릭 **설정** hello 오른쪽 탐색 창 아래에 **Facebook 로그인**</span><span class="sxs-lookup"><span data-stu-id="0afe9-129">Click **Settings** on hello right nav under **Facebook Login**</span></span>

    ![Facebook - Facebook 로그인 설정](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. <span data-ttu-id="0afe9-131">입력 `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` hello에 **유효한 OAuth 리디렉션 Uri** 필드 hello에 **클라이언트 OAuth 설정** 섹션.</span><span class="sxs-lookup"><span data-stu-id="0afe9-131">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Valid OAuth redirect URIs** field in hello **Client OAuth Settings** section.</span></span> <span data-ttu-id="0afe9-132">**{tenant}** 를 사용자의 테넌트 이름(예: contosob2c.onmicrosoft.com)으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-132">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="0afe9-133">클릭 **변경 내용 저장** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-133">Click **Save Changes** at hello bottom of hello page.</span></span>
    
    ![Facebook - OAuth 리디렉션 URI](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. <span data-ttu-id="0afe9-135">toomake Facebook 응용 프로그램 toomake 필요한 Azure AD B2C 하 여 사용할 수 있는, 공개적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-135">toomake your Facebook application usable by Azure AD B2C, you need toomake it publicly available.</span></span> <span data-ttu-id="0afe9-136">클릭 하 여이 작업을 수행할 수 **응용 프로그램 검토** 설정 hello와 왼쪽 탐색 hello에서 전환 hello hello 페이지 위쪽에 너무**예** 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-136">You can do this by clicking **App Review** on hello left navigation and by turning hello switch at hello top of hello page too**YES** and clicking **Confirm**.</span></span>
    
    ![Facebook - 앱 공개](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="0afe9-138">테넌트에서 Facebook을 ID 공급자로 구성</span><span class="sxs-lookup"><span data-stu-id="0afe9-138">Configure Facebook as an identity provider in your tenant</span></span>
1. <span data-ttu-id="0afe9-139">다음 단계를 너무[toohello B2C 기능 블레이드를 탐색](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure 포털에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-139">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="0afe9-140">Hello B2C 기능 블레이드에서 클릭 **Id 공급자**합니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-140">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="0afe9-141">클릭 **+ 추가** hello hello 블레이드 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-141">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="0afe9-142">친숙 한 제공 **이름** hello id 공급자 구성에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-142">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="0afe9-143">예를 들어 "Facebook"을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-143">For example, enter "Facebook".</span></span>
5. <span data-ttu-id="0afe9-144">**ID 공급자 형식**을 클릭하고 **Facebook**을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-144">Click **Identity provider type**, select **Facebook**, and click **OK**.</span></span>
6. <span data-ttu-id="0afe9-145">클릭 **이 id 공급자 설정** (hello 앞에서 만든 Facebook 응용 프로그램)의 hello 응용 프로그램 ID 및 앱 암호를 입력 하 고 hello에 **클라이언트 ID** 및 **클라이언트 암호**각각 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-145">Click **Set up this identity provider** and enter hello app ID and app secret (of hello Facebook application that you created earlier) in hello **Client ID** and **Client secret** fields respectively.</span></span>
7. <span data-ttu-id="0afe9-146">클릭 **확인**, 클릭 하 고 **만들기** toosave Facebook 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-146">Click **OK**, and then click **Create** toosave your Facebook configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="0afe9-147">추가 **Id 공급자** tooyour 테 넌 트 기존 정책을 수정 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-147">Adding an **Identity provider** tooyour tenant does not modify your existing policies.</span></span> <span data-ttu-id="0afe9-148">방금 만든 hello id 공급자를 포함 하 여 tooupdate 정책 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="0afe9-148">Remember tooupdate your policies by including hello identity provider you just created.</span></span>
>