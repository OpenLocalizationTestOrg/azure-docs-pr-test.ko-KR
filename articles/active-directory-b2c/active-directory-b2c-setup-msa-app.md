---
title: "Azure Active Directory B2C: Microsoft 계정 구성 | Microsoft Docs"
description: "소비자는 Azure Active Directory B2C에 의해 보호되는 응용 프로그램에서 Microsoft 계정으로 등록하고 로그인할 수 있습니다."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 06407322-142c-4cb3-9106-a8d752c4c853
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 59879dc0b3fc1d7af3e2a1f67f1701f451de9126
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-microsoft-accounts"></a><span data-ttu-id="4f93e-103">Azure Active Directory B2C: 고객에게 Microsoft 계정으로 등록 및 로그인 제공</span><span class="sxs-lookup"><span data-stu-id="4f93e-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Microsoft accounts</span></span>
## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="4f93e-104">Microsoft 계정 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="4f93e-104">Create a Microsoft account application</span></span>
<span data-ttu-id="4f93e-105">Azure AD(Active Directory) B2C에서 Microsoft 계정을 ID 공급자로 사용하려면 먼저 Microsoft 계정 응용 프로그램을 만들고 올바른 매개 변수를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f93e-105">To use Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Microsoft account application and supply it with the right parameters.</span></span> <span data-ttu-id="4f93e-106">이렇게 하려면 Microsoft 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4f93e-106">You need a Microsoft account to do this.</span></span> <span data-ttu-id="4f93e-107">계정이 없는 경우 [https://www.live.com/](https://www.live.com/)에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f93e-107">If you don’t have one, you can get it at [https://www.live.com/](https://www.live.com/).</span></span>

1. <span data-ttu-id="4f93e-108">[Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)로 이동하고 Microsoft 계정 자격 증명을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4f93e-108">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2. <span data-ttu-id="4f93e-109">**앱 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4f93e-109">Click **Add an app**.</span></span>
   
    ![Microsoft 계정 - 새 앱 추가](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. <span data-ttu-id="4f93e-111">응용 프로그램에 대한 **이름**을 제공하고 **응용 프로그램 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4f93e-111">Provide a **Name** for your application and click **Create application**.</span></span>
   
    ![Microsoft 계정 - 앱 이름](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. <span data-ttu-id="4f93e-113">**응용 프로그램 ID**의 값을 복사합니다. 테넌트에서 Microsoft 계정을 ID 공급자로 구성하려면 그 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4f93e-113">Copy the value of **Application Id**. You will need it to configure Microsoft account as an identity provider in your tenant.</span></span>
   
    ![Microsoft 계정 - 응용 프로그램 ID](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. <span data-ttu-id="4f93e-115">**플랫폼 추가**를 클릭하고 **웹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4f93e-115">Click on **Add platform** and choose **Web**.</span></span>
   
    ![Microsoft 계정 - 플랫폼 추가](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Microsoft 계정 - 웹](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. <span data-ttu-id="4f93e-118">**URI 리디렉션** 필드에 `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4f93e-118">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Redirect URIs** field.</span></span> <span data-ttu-id="4f93e-119">**{tenant}** 를 사용자의 테넌트 이름(예: contosob2c.onmicrosoft.com)으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4f93e-119">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
   
    ![Microsoft 계정 - URL 리디렉션](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. <span data-ttu-id="4f93e-121">**응용 프로그램 비밀** 섹션 아래에서 **새 암호 생성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4f93e-121">Click on **Generate New Password** under the **Application Secrets** section.</span></span> <span data-ttu-id="4f93e-122">화면에 표시되는 새 암호를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4f93e-122">Copy the new password displayed on screen.</span></span> <span data-ttu-id="4f93e-123">테넌트에서 Microsoft 계정을 ID 공급자로 구성하려면 그 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4f93e-123">You will need it to configure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="4f93e-124">이 암호는 중요한 보안 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="4f93e-124">This password is an important security credential.</span></span>
   
    ![Microsoft 계정-새 암호 생성](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Microsoft 계정-새 암호](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. <span data-ttu-id="4f93e-127">**고급 옵션** 섹션 아래에서 **Live SDK 지원**라는 상자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4f93e-127">Check the box that says **Live SDK support** under the **Advanced Options** section.</span></span> <span data-ttu-id="4f93e-128">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4f93e-128">Click **Save**.</span></span>
   
    ![Microsoft 계정-Live SDK 지원](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="4f93e-130">테넌트에서 Microsoft 계정을 ID 공급자로 구성</span><span class="sxs-lookup"><span data-stu-id="4f93e-130">Configure Microsoft account as an identity provider in your tenant</span></span>
1. <span data-ttu-id="4f93e-131">다음 단계에 따라 [Azure 포털의 B2C 기능 블레이드로 이동합니다](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) .</span><span class="sxs-lookup"><span data-stu-id="4f93e-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="4f93e-132">B2C 기능 블레이드에서 **ID 공급자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4f93e-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="4f93e-133">블레이드의 위쪽에서 **+추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4f93e-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="4f93e-134">ID 공급자 구성에 친숙한 **이름** 을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f93e-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="4f93e-135">예를 들어 "MSA"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4f93e-135">For example, enter "MSA".</span></span>
5. <span data-ttu-id="4f93e-136">**ID 공급자 형식**을 클릭하고 **Microsoft 계정**을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4f93e-136">Click **Identity provider type**, select **Microsoft account**, and click **OK**.</span></span>
6. <span data-ttu-id="4f93e-137">**이 ID 공급자 설정** 을 클릭하고 이전에 만든 Microsoft 계정 응용 프로그램의 응용 프로그램 ID 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4f93e-137">Click **Set up this identity provider** and enter the Application Id and password of the Microsoft account application that you created earlier.</span></span>
7. <span data-ttu-id="4f93e-138">**확인**을 클릭한 다음 **만들기**를 클릭하여 Microsoft 계정 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4f93e-138">Click **OK** and then click **Create** to save your Microsoft account configuration.</span></span>

