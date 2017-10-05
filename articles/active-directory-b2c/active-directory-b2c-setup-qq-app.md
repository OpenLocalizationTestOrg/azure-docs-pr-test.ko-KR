---
title: "Azure Active Directory B2C: QQ 구성 | Microsoft Docs"
description: "소비자에게 Azure Active Directory B2C를 사용하여 보안이 유지되는 응용 프로그램에서 QQ 계정으로 등록 및 로그인을 제공합니다."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 18c2cf94-8004-4de1-81c2-e45be65ce12d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: b32e81494b8c84799485f154ae43ad30af394caa
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-qq-accounts"></a><span data-ttu-id="555c6-103">Azure Active Directory B2C: 고객에게 QQ 계정으로 등록 및 로그인 제공</span><span class="sxs-lookup"><span data-stu-id="555c6-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with QQ accounts</span></span>

> [!NOTE]
> <span data-ttu-id="555c6-104">이 기능은 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-104">This feature is in preview.</span></span>
> 

## <a name="create-a-qq-application"></a><span data-ttu-id="555c6-105">QQ 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="555c6-105">Create a QQ application</span></span>

<span data-ttu-id="555c6-106">Azure AD(Azure Active Directory) B2C에서 QQ를 ID 공급자로 사용하려면 QQ 응용 프로그램을 만들고 올바른 매개 변수를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-106">To use QQ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a QQ application and supply it with the right parameters.</span></span> <span data-ttu-id="555c6-107">이렇게 하려면 QQ 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-107">You need a QQ account to do this.</span></span> <span data-ttu-id="555c6-108">없는 경우 [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033)에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-108">If you don’t have one, you can get one at [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span></span>

### <a name="register-for-the-qq-developer-program"></a><span data-ttu-id="555c6-109">QQ 개발자 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="555c6-109">Register for the QQ developer program</span></span>

1. <span data-ttu-id="555c6-110">[QQ 개발자 포털](http://open.qq.com)로 이동하고 QQ 계정 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-110">Go to the [QQ developer portal](http://open.qq.com) and sign in with your QQ account credentials.</span></span>
2. <span data-ttu-id="555c6-111">로그인한 후 [http://open.qq.com/reg](http://open.qq.com/reg)로 이동하여 개발자로서 사용자가 직접 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-111">After signing in, go to [http://open.qq.com/reg](http://open.qq.com/reg) to register yourself as a developer.</span></span>
3. <span data-ttu-id="555c6-112">메뉴에서 **个人**(개별 개발자)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-112">In the menu, select **个人** (individual developer).</span></span>
4. <span data-ttu-id="555c6-113">양식에 필요한 정보를 입력하고 **下一步**(다음 단계)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-113">Enter the required information into the form and click **下一步** (next step).</span></span>
5. <span data-ttu-id="555c6-114">전자 메일 확인 프로세스를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-114">Complete the email verification process.</span></span>

> [!NOTE]
> <span data-ttu-id="555c6-115">개발자로 등록한 후 승인이 되기까지 몇 일 동안 기다려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-115">You will need to wait a few days to be approved after registering as a developer.</span></span> 

### <a name="register-a-qq-application"></a><span data-ttu-id="555c6-116">QQ 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="555c6-116">Register a QQ application</span></span>

1. <span data-ttu-id="555c6-117">[https://connect.qq.com/index.html](https://connect.qq.com/index.html)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-117">Go to [https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span></span>
2. <span data-ttu-id="555c6-118">**应用管理**(앱 관리)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-118">Click on **应用管理** (app management).</span></span>
3. <span data-ttu-id="555c6-119">**创建应用**(앱 만들기)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-119">Click on **创建应用** (create app).</span></span>
4. <span data-ttu-id="555c6-120">필요한 앱 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-120">Enter the necessary app information.</span></span>
5. <span data-ttu-id="555c6-121">**创建应用**(앱 만들기)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-121">Click on **创建应用** (create app).</span></span>
6. <span data-ttu-id="555c6-122">필요한 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-122">Enter the required information.</span></span>
7. <span data-ttu-id="555c6-123">**授权回调域**(콜백 URL) 필드에 `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-123">For the **授权回调域** (callback URL) field, enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="555c6-124">예를 들어 `tenant_name`이 contoso.onmicrosoft.com인 경우 URL을 `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`가 되도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-124">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
8. <span data-ttu-id="555c6-125">**创建应用**(앱 만들기)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-125">Click on **创建应用** (create app).</span></span>
9. <span data-ttu-id="555c6-126">확인 페이지에서 **应用管理**(앱 관리)를 클릭하여 앱 관리 페이지로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-126">On the confirmation page, click on **应用管理** (app management) to return to the app management page.</span></span>
10. <span data-ttu-id="555c6-127">방금 만든 앱 옆에 있는 **查看**(보기)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-127">Click on **查看** (view) next to the app you just created.</span></span>
11. <span data-ttu-id="555c6-128">**修改**(편집)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-128">Click on **修改** (edit).</span></span>
12. <span data-ttu-id="555c6-129">페이지 맨 위에서 **앱 ID** 및 **앱 키**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-129">From the top of the page, copy the **APP ID** and **APP KEY**.</span></span>

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="555c6-130">테넌트에서 QQ를 ID 공급자로 구성</span><span class="sxs-lookup"><span data-stu-id="555c6-130">Configure QQ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="555c6-131">다음 단계에 따라 [Azure 포털의 B2C 기능 블레이드로 이동합니다](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) .</span><span class="sxs-lookup"><span data-stu-id="555c6-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="555c6-132">B2C 기능 블레이드에서 **ID 공급자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="555c6-133">블레이드의 위쪽에서 **+추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="555c6-134">ID 공급자 구성에 친숙한 **이름** 을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="555c6-135">예를 들어 "QQ"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-135">For example, enter "QQ".</span></span>
5. <span data-ttu-id="555c6-136">**ID 공급자 형식**을 클릭하고 **QQ**를 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-136">Click **Identity provider type**, select **QQ**, and click **OK**.</span></span>
6. <span data-ttu-id="555c6-137">**이 ID 공급자 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-137">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="555c6-138">**클라이언트 ID**로 앞에서 복사한 **앱 키**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-138">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="555c6-139">**클라이언트 암호**로 앞에서 복사한 **앱 암호**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-139">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="555c6-140">**확인**을 클릭한 다음 **만들기**를 클릭하여 QQ 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="555c6-140">Click **OK** and then click **Create** to save your QQ configuration.</span></span>

