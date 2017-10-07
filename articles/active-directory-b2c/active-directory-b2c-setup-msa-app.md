---
title: "Azure Active Directory B2C: Microsoft 계정 구성 | Microsoft Docs"
description: "Azure Active Directory B2C에 의해 보안 되는 응용 프로그램에서 Microsoft 계정에 등록 및 로그인 tooconsumers를 제공 합니다."
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
ms.openlocfilehash: bec4777f003c459030f68c35b24f0e4bcddf84ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-microsoft-accounts"></a><span data-ttu-id="b6690-103">Azure Active Directory B2C: Microsoft 계정에 등록 및 로그인 tooconsumers 제공</span><span class="sxs-lookup"><span data-stu-id="b6690-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Microsoft accounts</span></span>
## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="b6690-104">Microsoft 계정 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="b6690-104">Create a Microsoft account application</span></span>
<span data-ttu-id="b6690-105">(Azure AD) Azure Active Directory B2C에 대 한 id 공급자로 toouse Microsoft 계정, Microsoft 계정 응용 프로그램 toocreate 필요 하 고 hello 오른쪽 매개 변수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6690-105">toouse Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Microsoft account application and supply it with hello right parameters.</span></span> <span data-ttu-id="b6690-106">사용자는 Microsoft 계정 toodo이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b6690-106">You need a Microsoft account toodo this.</span></span> <span data-ttu-id="b6690-107">계정이 없는 경우 [https://www.live.com/](https://www.live.com/)에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6690-107">If you don’t have one, you can get it at [https://www.live.com/](https://www.live.com/).</span></span>

1. <span data-ttu-id="b6690-108">Toohello 이동 [Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) Microsoft 계정 자격 증명으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6690-108">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2. <span data-ttu-id="b6690-109">**앱 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6690-109">Click **Add an app**.</span></span>
   
    ![Microsoft 계정 - 새 앱 추가](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. <span data-ttu-id="b6690-111">응용 프로그램에 대한 **이름**을 제공하고 **응용 프로그램 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6690-111">Provide a **Name** for your application and click **Create application**.</span></span>
   
    ![Microsoft 계정 - 앱 이름](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. <span data-ttu-id="b6690-113">hello 값을 복사 **응용 프로그램 Id**합니다. 필요 tooconfigure Microsoft 계정을 id 공급자로 테 넌 트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6690-113">Copy hello value of **Application Id**. You will need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span>
   
    ![Microsoft 계정 - 응용 프로그램 ID](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. <span data-ttu-id="b6690-115">**플랫폼 추가**를 클릭하고 **웹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6690-115">Click on **Add platform** and choose **Web**.</span></span>
   
    ![Microsoft 계정 - 플랫폼 추가](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Microsoft 계정 - 웹](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. <span data-ttu-id="b6690-118">입력 `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` hello에 **리디렉션 Uri** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="b6690-118">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Redirect URIs** field.</span></span> <span data-ttu-id="b6690-119">**{tenant}** 를 사용자의 테넌트 이름(예: contosob2c.onmicrosoft.com)으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b6690-119">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
   
    ![Microsoft 계정 - URL 리디렉션](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. <span data-ttu-id="b6690-121">클릭 **새 암호를 생성할** hello에서 **응용 프로그램 암호** 섹션.</span><span class="sxs-lookup"><span data-stu-id="b6690-121">Click on **Generate New Password** under hello **Application Secrets** section.</span></span> <span data-ttu-id="b6690-122">Hello 화면에 표시 되는 새 암호를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6690-122">Copy hello new password displayed on screen.</span></span> <span data-ttu-id="b6690-123">필요 tooconfigure Microsoft 계정을 id 공급자로 테 넌 트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6690-123">You will need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="b6690-124">이 암호는 중요한 보안 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="b6690-124">This password is an important security credential.</span></span>
   
    ![Microsoft 계정-새 암호 생성](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Microsoft 계정-새 암호](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. <span data-ttu-id="b6690-127">Hello 확인란의 **라이브 SDK 지원** hello에서 **고급 옵션** 섹션.</span><span class="sxs-lookup"><span data-stu-id="b6690-127">Check hello box that says **Live SDK support** under hello **Advanced Options** section.</span></span> <span data-ttu-id="b6690-128">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6690-128">Click **Save**.</span></span>
   
    ![Microsoft 계정-Live SDK 지원](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="b6690-130">테넌트에서 Microsoft 계정을 ID 공급자로 구성</span><span class="sxs-lookup"><span data-stu-id="b6690-130">Configure Microsoft account as an identity provider in your tenant</span></span>
1. <span data-ttu-id="b6690-131">다음 단계를 너무[toohello B2C 기능 블레이드를 탐색](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure 포털에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6690-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="b6690-132">Hello B2C 기능 블레이드에서 클릭 **Id 공급자**합니다.</span><span class="sxs-lookup"><span data-stu-id="b6690-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="b6690-133">클릭 **+ 추가** hello hello 블레이드 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6690-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="b6690-134">친숙 한 제공 **이름** hello id 공급자 구성에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6690-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="b6690-135">예를 들어 "MSA"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b6690-135">For example, enter "MSA".</span></span>
5. <span data-ttu-id="b6690-136">**ID 공급자 형식**을 클릭하고 **Microsoft 계정**을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6690-136">Click **Identity provider type**, select **Microsoft account**, and click **OK**.</span></span>
6. <span data-ttu-id="b6690-137">클릭 **이 id 공급자 설정** hello 응용 프로그램 Id 및 hello 앞에서 만든 Microsoft 계정 응용 프로그램의 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6690-137">Click **Set up this identity provider** and enter hello Application Id and password of hello Microsoft account application that you created earlier.</span></span>
7. <span data-ttu-id="b6690-138">클릭 **확인** 클릭 하 고 **만들기** toosave Microsoft 계정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6690-138">Click **OK** and then click **Create** toosave your Microsoft account configuration.</span></span>

