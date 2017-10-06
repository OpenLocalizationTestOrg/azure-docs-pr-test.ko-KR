---
title: "Azure Active Directory B2C: Weibo 구성 | Microsoft Docs"
description: "등록 및 로그인 tooconsumers Weibo 계정 Azure Active Directory B2C에 의해 보안 되는 응용 프로그램에 제공 합니다."
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
ms.openlocfilehash: c0648620f318046c1d9d24feb92a0c5f19c6a91a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-weibo-accounts"></a><span data-ttu-id="8ac54-103">Azure Active Directory B2C: Weibo 계정 등록 및 로그인 tooconsumers 제공</span><span class="sxs-lookup"><span data-stu-id="8ac54-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Weibo accounts</span></span>

> [!NOTE]
> <span data-ttu-id="8ac54-104">이 기능은 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-104">This feature is in preview.</span></span> <span data-ttu-id="8ac54-105">프로덕션 환경에서는 이 ID 공급자를 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="8ac54-105">Do not use this identity provider in your production environment.</span></span>
> 

## <a name="create-a-weibo-application"></a><span data-ttu-id="8ac54-106">Weibo 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="8ac54-106">Create a Weibo application</span></span>

<span data-ttu-id="8ac54-107">toouse Weibo (Azure AD) Azure Active Directory B2C에을 id 공급자로 toocreate Weibo 응용 프로그램에 필요 하 고이 hello 오른쪽 매개 변수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-107">toouse Weibo as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Weibo application and supply it with hello right parameters.</span></span> <span data-ttu-id="8ac54-108">하면 Weibo 계정 toodo이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-108">You need a Weibo account toodo this.</span></span> <span data-ttu-id="8ac54-109">없는 경우 [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us)에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-109">If you don’t have one, you can get one at [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span></span>

### <a name="register-for-hello-weibo-developer-program"></a><span data-ttu-id="8ac54-110">Hello Weibo 개발자 프로그램에 대 한 등록</span><span class="sxs-lookup"><span data-stu-id="8ac54-110">Register for hello Weibo developer program</span></span>

1. <span data-ttu-id="8ac54-111">Toohello 이동 [Weibo 개발자 포털](http://open.weibo.com/) Weibo 계정 자격 증명으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-111">Go toohello [Weibo developer portal](http://open.weibo.com/) and sign in with your Weibo account credentials.</span></span>
2. <span data-ttu-id="8ac54-112">로그인 한 후 hello 오른쪽 위 모서리에는 표시 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-112">After signing in, click on your display name in hello top-right corner.</span></span>
3. <span data-ttu-id="8ac54-113">Hello 드롭다운에서 선택**编辑开发者信息**(개발자 정보 편집).</span><span class="sxs-lookup"><span data-stu-id="8ac54-113">In hello dropdown, select **编辑开发者信息** (edit developer information).</span></span>
4. <span data-ttu-id="8ac54-114">Hello 양식으로 hello 필요한 정보를 입력 하 고 클릭**提交**(전송) 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-114">Enter hello required information into hello form and click **提交** (submit).</span></span>
5. <span data-ttu-id="8ac54-115">Hello 전자 메일 확인 프로세스를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-115">Complete hello email verification process.</span></span>
6. <span data-ttu-id="8ac54-116">Toohello 이동 [id 확인 페이지](http://open.weibo.com/developers/identity/edit)합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-116">Go toohello [identity verification page](http://open.weibo.com/developers/identity/edit).</span></span>
7. <span data-ttu-id="8ac54-117">Hello 양식으로 hello 필요한 정보를 입력 하 고 클릭**提交**(전송) 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-117">Enter hello required information into hello form and click **提交** (submit).</span></span>

### <a name="register-a-weibo-application"></a><span data-ttu-id="8ac54-118">Weibo 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="8ac54-118">Register a Weibo application</span></span>

1. <span data-ttu-id="8ac54-119">Toohello 이동 [새 Weibo 응용 프로그램 등록 페이지](http://open.weibo.com/apps/new)합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-119">Go toohello [new Weibo app registration page](http://open.weibo.com/apps/new).</span></span>
2. <span data-ttu-id="8ac54-120">Hello 필요한 응용 프로그램 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-120">Enter hello necessary application information.</span></span>
3. <span data-ttu-id="8ac54-121">**创 建**(만들기)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-121">Click **创建** (create).</span></span>
4. <span data-ttu-id="8ac54-122">Hello 값의 복사 **응용 프로그램 키는** 및 **응용 프로그램 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-122">Copy hello values of **App Key** and **App Secret**.</span></span> <span data-ttu-id="8ac54-123">이 ID는 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-123">You will need this later.</span></span>
5. <span data-ttu-id="8ac54-124">필요한 hello 사진을 업로드 하 고 hello 필요한 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-124">Upload hello required photos and enter hello necessary information.</span></span>
6. <span data-ttu-id="8ac54-125">**保存以上信息**(저장)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-125">Click **保存以上信息** (save).</span></span>
7. <span data-ttu-id="8ac54-126">**高级信息**(고급 정보)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-126">Click **高级信息** (advanced information).</span></span>
8. <span data-ttu-id="8ac54-127">클릭**编辑**oauth 2.0에 대 한 다음 toohello 필드 (편집)**授权设置**(URL 리디렉션).</span><span class="sxs-lookup"><span data-stu-id="8ac54-127">Click **编辑** (edit) next toohello field for OAuth2.0 **授权设置** (redirect URL).</span></span>
9. <span data-ttu-id="8ac54-128">OAuth2.0 **授权设置**(리디렉션 URL)에 `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-128">Enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` for OAuth2.0 **授权设置** (redirect URL).</span></span> <span data-ttu-id="8ac54-129">예를 들어 경우 프로그램 `tenant_name` contoso.onmicrosoft.com 집합 hello URL toobe은 `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-129">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
10. <span data-ttu-id="8ac54-130">**提交**(제출)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-130">Click **提交** (submit).</span></span>  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="8ac54-131">테넌트에서 Weibo를 ID 공급자로 구성</span><span class="sxs-lookup"><span data-stu-id="8ac54-131">Configure Weibo as an identity provider in your tenant</span></span>
1. <span data-ttu-id="8ac54-132">다음 단계를 너무[toohello B2C 기능 블레이드를 탐색](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure 포털에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-132">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="8ac54-133">Hello B2C 기능 블레이드에서 클릭 **Id 공급자**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-133">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="8ac54-134">클릭 **+ 추가** hello hello 블레이드 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-134">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="8ac54-135">친숙 한 제공 **이름** hello id 공급자 구성에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-135">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="8ac54-136">예를 들어 "Weibo"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-136">For example, enter "Weibo".</span></span>
5. <span data-ttu-id="8ac54-137">**ID 공급자 형식**을 클릭하고 **Weibo**를 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-137">Click **Identity provider type**, select **Weibo**, and click **OK**.</span></span>
6. <span data-ttu-id="8ac54-138">**이 ID 공급자 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-138">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="8ac54-139">Hello 입력 **응용 프로그램 키는** hello로 앞에서 복사한 **클라이언트 ID**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-139">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="8ac54-140">Hello 입력 **응용 프로그램 암호** hello로 앞에서 복사한 **클라이언트 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-140">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="8ac54-141">클릭 **확인** 클릭 하 고 **만들기** toosave Weibo 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac54-141">Click **OK** and then click **Create** toosave your Weibo configuration.</span></span>

