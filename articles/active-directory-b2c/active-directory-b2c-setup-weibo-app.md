---
title: "Azure Active Directory B2C: Weibo 구성 | Microsoft Docs"
description: "소비자에게 Azure Active Directory B2C를 사용하여 보안이 유지되는 응용 프로그램에서 Weibo 계정으로 등록 및 로그인을 제공합니다."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1860de34-94cb-4ceb-851e-102f930f7230
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 00c5d3781455c80b33bdbb4c872ae354531baf3e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-weibo-accounts"></a><span data-ttu-id="a9c2d-103">Azure Active Directory B2C: 고객에게 Weibo 계정으로 등록 및 로그인 제공</span><span class="sxs-lookup"><span data-stu-id="a9c2d-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Weibo accounts</span></span>

> [!NOTE]
> <span data-ttu-id="a9c2d-104">이 기능은 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-104">This feature is in preview.</span></span> <span data-ttu-id="a9c2d-105">프로덕션 환경에서는 이 ID 공급자를 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-105">Do not use this identity provider in your production environment.</span></span>
> 

## <a name="create-a-weibo-application"></a><span data-ttu-id="a9c2d-106">Weibo 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="a9c2d-106">Create a Weibo application</span></span>

<span data-ttu-id="a9c2d-107">Azure AD(Azure Active Directory) B2C에서 Weibo를 ID 공급자로 사용하려면 Weibo 응용 프로그램을 만들고 올바른 매개 변수를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-107">To use Weibo as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Weibo application and supply it with the right parameters.</span></span> <span data-ttu-id="a9c2d-108">이렇게 하려면 Weibo 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-108">You need a Weibo account to do this.</span></span> <span data-ttu-id="a9c2d-109">없는 경우 [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us)에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-109">If you don’t have one, you can get one at [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span></span>

### <a name="register-for-the-weibo-developer-program"></a><span data-ttu-id="a9c2d-110">Weibo 개발자 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="a9c2d-110">Register for the Weibo developer program</span></span>

1. <span data-ttu-id="a9c2d-111">[Weibo 개발자 포털](http://open.weibo.com/)로 이동하고 Weibo 계정 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-111">Go to the [Weibo developer portal](http://open.weibo.com/) and sign in with your Weibo account credentials.</span></span>
2. <span data-ttu-id="a9c2d-112">로그인한 후 오른쪽 위 모서리의 표시 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-112">After signing in, click on your display name in the top-right corner.</span></span>
3. <span data-ttu-id="a9c2d-113">드롭다운에서 **编辑开发者信息**(개발자 정보 편집)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-113">In the dropdown, select **编辑开发者信息** (edit developer information).</span></span>
4. <span data-ttu-id="a9c2d-114">양식에 필요한 정보를 입력하고 **提交**(제출)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-114">Enter the required information into the form and click **提交** (submit).</span></span>
5. <span data-ttu-id="a9c2d-115">전자 메일 확인 프로세스를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-115">Complete the email verification process.</span></span>
6. <span data-ttu-id="a9c2d-116">[ID 확인 페이지](http://open.weibo.com/developers/identity/edit)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-116">Go to the [identity verification page](http://open.weibo.com/developers/identity/edit).</span></span>
7. <span data-ttu-id="a9c2d-117">양식에 필요한 정보를 입력하고 **提交**(제출)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-117">Enter the required information into the form and click **提交** (submit).</span></span>

### <a name="register-a-weibo-application"></a><span data-ttu-id="a9c2d-118">Weibo 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="a9c2d-118">Register a Weibo application</span></span>

1. <span data-ttu-id="a9c2d-119">[새 Weibo 앱 등록 페이지](http://open.weibo.com/apps/new)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-119">Go to the [new Weibo app registration page](http://open.weibo.com/apps/new).</span></span>
2. <span data-ttu-id="a9c2d-120">필요한 응용 프로그램 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-120">Enter the necessary application information.</span></span>
3. <span data-ttu-id="a9c2d-121">**创 建**(만들기)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-121">Click **创建** (create).</span></span>
4. <span data-ttu-id="a9c2d-122">**앱 키** 및 **앱 암호**의 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-122">Copy the values of **App Key** and **App Secret**.</span></span> <span data-ttu-id="a9c2d-123">이 ID는 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-123">You will need this later.</span></span>
5. <span data-ttu-id="a9c2d-124">필요한 사진을 업로드하고 필요한 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-124">Upload the required photos and enter the necessary information.</span></span>
6. <span data-ttu-id="a9c2d-125">**保存以上信息**(저장)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-125">Click **保存以上信息** (save).</span></span>
7. <span data-ttu-id="a9c2d-126">**高级信息**(고급 정보)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-126">Click **高级信息** (advanced information).</span></span>
8. <span data-ttu-id="a9c2d-127">OAuth2.0 **授权设置**(리디렉션 URL)에 대한 필드 옆의 **编辑**(편집)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-127">Click **编辑** (edit) next to the field for OAuth2.0 **授权设置** (redirect URL).</span></span>
9. <span data-ttu-id="a9c2d-128">OAuth2.0 **授权设置**(리디렉션 URL)에 `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-128">Enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` for OAuth2.0 **授权设置** (redirect URL).</span></span> <span data-ttu-id="a9c2d-129">예를 들어 `tenant_name`이 contoso.onmicrosoft.com인 경우 URL을 `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`가 되도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-129">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
10. <span data-ttu-id="a9c2d-130">**提交**(제출)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-130">Click **提交** (submit).</span></span>  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="a9c2d-131">테넌트에서 Weibo를 ID 공급자로 구성</span><span class="sxs-lookup"><span data-stu-id="a9c2d-131">Configure Weibo as an identity provider in your tenant</span></span>
1. <span data-ttu-id="a9c2d-132">다음 단계에 따라 [Azure 포털의 B2C 기능 블레이드로 이동합니다](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) .</span><span class="sxs-lookup"><span data-stu-id="a9c2d-132">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="a9c2d-133">B2C 기능 블레이드에서 **ID 공급자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-133">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="a9c2d-134">블레이드의 위쪽에서 **+추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-134">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="a9c2d-135">ID 공급자 구성에 친숙한 **이름** 을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-135">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="a9c2d-136">예를 들어 "Weibo"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-136">For example, enter "Weibo".</span></span>
5. <span data-ttu-id="a9c2d-137">**ID 공급자 형식**을 클릭하고 **Weibo**를 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-137">Click **Identity provider type**, select **Weibo**, and click **OK**.</span></span>
6. <span data-ttu-id="a9c2d-138">**이 ID 공급자 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-138">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="a9c2d-139">**클라이언트 ID**로 앞에서 복사한 **앱 키**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-139">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="a9c2d-140">**클라이언트 암호**로 앞에서 복사한 **앱 암호**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-140">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="a9c2d-141">**확인**을 클릭한 다음 **만들기**를 클릭하여 Weibo 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c2d-141">Click **OK** and then click **Create** to save your Weibo configuration.</span></span>

