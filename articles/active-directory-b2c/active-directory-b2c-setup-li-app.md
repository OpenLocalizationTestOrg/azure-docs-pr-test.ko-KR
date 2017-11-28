---
title: "Azure Active Directory B2C: LinkedIn 구성 | Microsoft Docs"
description: "Azure Active Directory B2C에 의해 보안 되는 응용 프로그램에서 LinkedIn 계정 등록 및 로그인 tooconsumers 제공"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: fa51a16b-9ce9-4e27-9eff-0869b4c4f0ef
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6c5233ef48b24968fd6383f470b5d8a969a78ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-linkedin-accounts"></a><span data-ttu-id="f95ee-103">Azure Active Directory B2C: LinkedIn 계정 등록 및 로그인 tooconsumers 제공</span><span class="sxs-lookup"><span data-stu-id="f95ee-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with LinkedIn accounts</span></span>
## <a name="create-a-linkedin-application"></a><span data-ttu-id="f95ee-104">LinkedIn 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="f95ee-104">Create a LinkedIn application</span></span>
<span data-ttu-id="f95ee-105">LinkedIn toouse (Azure AD) Azure Active Directory B2C에을 id 공급자로 toocreate LinkedIn 응용 프로그램에 필요 하 고이 hello 오른쪽 매개 변수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ee-105">toouse LinkedIn as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a LinkedIn application and supply it with hello right parameters.</span></span> <span data-ttu-id="f95ee-106">하면 LinkedIn 계정 toodo이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ee-106">You need a LinkedIn account toodo this.</span></span> <span data-ttu-id="f95ee-107">계정이 없는 경우 [https://www.linkedin.com/](https://www.linkedin.com/)에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ee-107">If you don’t have one, you can get it at [https://www.linkedin.com/](https://www.linkedin.com/).</span></span>

1. <span data-ttu-id="f95ee-108">Toohello 이동 [LinkedIn 개발자 웹 사이트](https://www.developer.linkedin.com/) LinkedIn 계정 자격 증명으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ee-108">Go toohello [LinkedIn Developers website](https://www.developer.linkedin.com/) and sign in with your LinkedIn account credentials.</span></span>
2. <span data-ttu-id="f95ee-109">클릭 **My Apps** 상단 메뉴 모음 hello와 클릭 **응용 프로그램 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ee-109">Click **My Apps** in hello top menu bar and then click **Create Application**.</span></span>
   
    ![LinkedIn - 새 앱](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. <span data-ttu-id="f95ee-111">Hello에 **새 응용 프로그램 만들기** 양식에서 hello 관련 정보를 입력 (**회사 이름**, **이름**, **설명**, **응용 프로그램 로고 URL**, **응용 프로그램 사용**, **웹 사이트 URL**, **비즈니스 메일** 및 **회사전화**).</span><span class="sxs-lookup"><span data-stu-id="f95ee-111">In hello **Create a New Application** form, fill in hello relevant information (**Company Name**, **Name**, **Description**, **Application Logo URL**, **Application Use**, **Website URL**, **Business Email** and **Business Phone**).</span></span>
4. <span data-ttu-id="f95ee-112">Toohello 동의 **LinkedIn 사용 약관 API** 클릭 **전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ee-112">Agree toohello **LinkedIn API Terms of Use** and click **Submit**.</span></span>
   
    ![LinkedIn - 앱 등록](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. <span data-ttu-id="f95ee-114">Hello 값의 복사 **클라이언트 ID** 및 **클라이언트 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ee-114">Copy hello values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="f95ee-115">(**인증 키** 아래에서 찾을 수 있습니다.) 둘 모두 필요 합니다 tooconfigure 테 넌 트를 id 공급자로 LinkedIn 합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ee-115">(You can find them under **Authentication Keys**.) You will need both of them tooconfigure LinkedIn as an identity provider in your tenant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f95ee-116">**클라이언트 암호** 는 중요한 보안 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="f95ee-116">**Client Secret** is an important security credential.</span></span>
   > 
   > 
6. <span data-ttu-id="f95ee-117">입력 `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` hello에 **리디렉션 Url 권한이** 필드 (아래 **OAuth 2.0**).</span><span class="sxs-lookup"><span data-stu-id="f95ee-117">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized Redirect URLs** field (under **OAuth 2.0**).</span></span> <span data-ttu-id="f95ee-118">**{tenant}** 를 사용자의 테넌트 이름(예: contoso.onmicrosoft.com)으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f95ee-118">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="f95ee-119">**추가**를 클릭한 후 **업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ee-119">Click **Add**, and then click **Update**.</span></span> <span data-ttu-id="f95ee-120">hello **{tenant}** 값은 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ee-120">hello **{tenant}** value is case-sensitive.</span></span>
   
    ![LinkedIn - 앱 설정](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="f95ee-122">테넌트에서 LinkedIn을 ID 공급자로 구성</span><span class="sxs-lookup"><span data-stu-id="f95ee-122">Configure LinkedIn as an identity provider in your tenant</span></span>
1. <span data-ttu-id="f95ee-123">다음 단계를 너무[toohello B2C 기능 블레이드를 탐색](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure 포털에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ee-123">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="f95ee-124">Hello B2C 기능 블레이드에서 클릭 **Id 공급자**합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ee-124">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="f95ee-125">클릭 **+ 추가** hello hello 블레이드 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ee-125">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="f95ee-126">친숙 한 제공 **이름** hello id 공급자 구성에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ee-126">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="f95ee-127">예를 들어 "LI"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ee-127">For example, enter "LI".</span></span>
5. <span data-ttu-id="f95ee-128">**ID 공급자 형식**을 클릭하고 **LinkedIn**을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ee-128">Click **Identity provider type**, select **LinkedIn**, and click **OK**.</span></span>
6. <span data-ttu-id="f95ee-129">클릭 **이 id 공급자 설정** hello 앞에서 만든 LinkedIn 응용 프로그램의 hello 클라이언트 ID와 클라이언트 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ee-129">Click **Set up this identity provider** and enter hello client ID and client secret of hello LinkedIn application that you created earlier.</span></span>
7. <span data-ttu-id="f95ee-130">클릭 **확인** 클릭 하 고 **만들기** toosave LinkedIn 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ee-130">Click **OK** and then click **Create** toosave your LinkedIn configuration.</span></span>

