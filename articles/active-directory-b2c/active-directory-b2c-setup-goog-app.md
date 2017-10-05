---
title: "Azure Active Directory B2C: Google+ 구성 | Microsoft Docs"
description: "소비자에게 Azure Active Directory B2C를 사용하여 보안이 유지되는 응용 프로그램에서 Google+ 계정으로 등록 및 로그인을 제공합니다."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 4dcca66f-29e4-4b4d-8840-50baad736bd7
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6ab73e5c79742ab548733f5712dee1e28461db9f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-google-accounts"></a><span data-ttu-id="da426-103">Azure Active Directory B2C: 고객에게 Google+ 계정으로 등록 및 로그인 제공</span><span class="sxs-lookup"><span data-stu-id="da426-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Google+ accounts</span></span>
## <a name="create-a-google-application"></a><span data-ttu-id="da426-104">Google+ 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="da426-104">Create a Google+ application</span></span>
<span data-ttu-id="da426-105">Azure AD(Azure Active Directory) B2C에서 Google+를 ID 공급자로 사용하려면 Google+ 응용 프로그램을 만들고 올바른 매개 변수를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da426-105">To use Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Google+ application and supply it with the right parameters.</span></span> <span data-ttu-id="da426-106">이렇게 하려면 Google+ 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="da426-106">You need a Google+ account to do this.</span></span> <span data-ttu-id="da426-107">계정이 없으면 [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da426-107">If you don’t have one, you can get it at [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span></span>

1. <span data-ttu-id="da426-108">[Google 개발자 콘솔](https://console.developers.google.com/) 로 이동하고 Google + 계정 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="da426-108">Go to the [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2. <span data-ttu-id="da426-109">**프로젝트 만들기**를 클릭하고 **프로젝트 이름**을 입력한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da426-109">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>
   
    ![Google+ - 시작](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google+ - 새 프로젝트](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. <span data-ttu-id="da426-112">**API 관리자**를 클릭한 다음 왼쪽 탐색에서 **자격 증명**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da426-112">Click **API Manager** and then click **Credentials** in the left navigation.</span></span>
4. <span data-ttu-id="da426-113">**OAuth 동의 화면**을 위쪽 탭에서 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da426-113">Click the **OAuth consent screen** tab at the top.</span></span>
   
    ![Google+ - 자격 증명](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. <span data-ttu-id="da426-115">유효한 **메일 주소**를 선택하거나 지정하고 **제품 이름**을 제공한 후 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da426-115">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>
   
    ![Google+ - OAuth 동의 화면](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. <span data-ttu-id="da426-117">**새 자격 증명**을 클릭한 다음 **OAuth 클라이언트 ID**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da426-117">Click **New credentials** and then choose **OAuth client ID**.</span></span>
   
    ![Google+ - OAuth 동의 화면](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. <span data-ttu-id="da426-119">**응용 프로그램 형식**에서 **웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da426-119">Under **Application type**, select **Web application**.</span></span>
   
    ![Google+ - OAuth 동의 화면](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. <span data-ttu-id="da426-121">응용 프로그램에 대한 **이름**을 제공하고 **권한이 부여된 JavaScript 원본** 필드에 `https://login.microsoftonline.com`을 입력하고 **권한이 부여된 리디렉션 URI** 필드에 `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="da426-121">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in the **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized redirect URIs** field.</span></span> <span data-ttu-id="da426-122">**{tenant}** 를 사용자의 테넌트 이름(예: contosob2c.onmicrosoft.com)으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="da426-122">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="da426-123">**{tenant}** 값은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="da426-123">The **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="da426-124">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da426-124">Click **Create**.</span></span>
   
    ![Google+ - 클라이언트 ID 만들기](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. <span data-ttu-id="da426-126">**클라이언트 ID** 및 **클라이언트 비밀** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="da426-126">Copy the values of **Client ID** and **Client secret**.</span></span> <span data-ttu-id="da426-127">테넌트에서 Google+를 ID 공급자로 구성하려면 둘 모두가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="da426-127">You will need both of them to configure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="da426-128">**클라이언트 암호** 는 중요한 보안 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="da426-128">**Client secret** is an important security credential.</span></span>
   
    ![Google+ - 클라이언트 암호](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="da426-130">테넌트에서 Google+를 ID 공급자로 구성</span><span class="sxs-lookup"><span data-stu-id="da426-130">Configure Google+ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="da426-131">다음 단계에 따라 [Azure 포털의 B2C 기능 블레이드로 이동합니다](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) .</span><span class="sxs-lookup"><span data-stu-id="da426-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="da426-132">B2C 기능 블레이드에서 **ID 공급자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da426-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="da426-133">블레이드의 위쪽에서 **+추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da426-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="da426-134">ID 공급자 구성에 친숙한 **이름** 을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="da426-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="da426-135">예를 들어 "G+"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="da426-135">For example, enter "G+".</span></span>
5. <span data-ttu-id="da426-136">**ID 공급자 형식**을 클릭하고 **Google**을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da426-136">Click **Identity provider type**, select **Google**, and click **OK**.</span></span>
6. <span data-ttu-id="da426-137">**이 ID 공급자 설정**을 클릭하고 이전에 만든 Google+ 응용 프로그램의 클라이언트 ID 및 클라이언트 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="da426-137">Click **Set up this identity provider** and enter the client ID and client secret of the Google+ application that you created earlier.</span></span>
7. <span data-ttu-id="da426-138">**확인**을 클릭한 다음 **만들기**를 클릭하여 Google+ 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="da426-138">Click **OK** and then click **Create** to save your Google+ configuration.</span></span>

