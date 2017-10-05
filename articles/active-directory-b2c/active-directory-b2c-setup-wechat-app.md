---
title: "Azure Active Directory B2C: WeChat 구성 | Microsoft Docs"
description: "소비자에게 Azure Active Directory B2C를 사용하여 보안이 유지되는 응용 프로그램에서 WeChat 계정으로 등록 및 로그인을 제공합니다."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d2424c66-ba68-4d82-847e-d137683527b0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: a54aec23d951610118246e9f70cdd27752ef39a6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-wechat-accounts"></a><span data-ttu-id="d4f06-103">Azure Active Directory B2C: 고객에게 WeChat 계정으로 등록 및 로그인 제공</span><span class="sxs-lookup"><span data-stu-id="d4f06-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with WeChat accounts</span></span>

> [!NOTE]
> <span data-ttu-id="d4f06-104">이 기능은 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="d4f06-104">This feature is in preview.</span></span>
> 

## <a name="create-a-wechat-application"></a><span data-ttu-id="d4f06-105">WeChat 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="d4f06-105">Create a WeChat application</span></span>

<span data-ttu-id="d4f06-106">Azure AD(Azure Active Directory) B2C에서 WeChat을 ID 공급자로 사용하려면 WeChat 응용 프로그램을 만들고 올바른 매개 변수를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f06-106">To use WeChat as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a WeChat application and supply it with the right parameters.</span></span> <span data-ttu-id="d4f06-107">이렇게 하려면 WeChat 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f06-107">You need a WeChat account to do this.</span></span> <span data-ttu-id="d4f06-108">없는 경우 모바일 앱 중 하나를 통해 등록하거나 QQ 번호를 사용하여 하나를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4f06-108">If you don’t have one, you can get one by signing up through one of their mobile apps or by using your QQ number.</span></span> <span data-ttu-id="d4f06-109">그 후에 WeChat 개발자 프로그램에 등록된 계정을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d4f06-109">After that, get your account registered with the WeChat developer program.</span></span> <span data-ttu-id="d4f06-110">자세한 내용은 [여기](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4f06-110">You can find more information [here](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span></span>

### <a name="register-a-wechat-application"></a><span data-ttu-id="d4f06-111">WeChat 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="d4f06-111">Register a WeChat application</span></span>

1. <span data-ttu-id="d4f06-112">[https://open.weixin.qq.com/](https://open.weixin.qq.com/)으로 이동하고 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f06-112">Go to [https://open.weixin.qq.com/](https://open.weixin.qq.com/) and log in.</span></span>
2. <span data-ttu-id="d4f06-113">**管理中心**(관리 센터)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f06-113">Click on **管理中心** (management center).</span></span>
3. <span data-ttu-id="d4f06-114">새 응용 프로그램을 등록하는 데 필요한 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d4f06-114">Follow the necessary steps to register a new application.</span></span>
4. <span data-ttu-id="d4f06-115">**授权回调域**(콜백 URL)에 `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f06-115">For **授权回调域** (callback URL), enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="d4f06-116">예를 들어 `tenant_name`이 contoso.onmicrosoft.com인 경우 URL을 `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`가 되도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f06-116">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
5. <span data-ttu-id="d4f06-117">**앱 ID** 및 **앱 키**를 찾고 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f06-117">Find and copy the **APP ID** and **APP KEY**.</span></span> <span data-ttu-id="d4f06-118">나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f06-118">You will need these later.</span></span>

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="d4f06-119">테넌트에서 WeChat을 ID 공급자로 구성</span><span class="sxs-lookup"><span data-stu-id="d4f06-119">Configure WeChat as an identity provider in your tenant</span></span>
1. <span data-ttu-id="d4f06-120">다음 단계에 따라 [Azure 포털의 B2C 기능 블레이드로 이동합니다](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) .</span><span class="sxs-lookup"><span data-stu-id="d4f06-120">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="d4f06-121">B2C 기능 블레이드에서 **ID 공급자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f06-121">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="d4f06-122">블레이드의 위쪽에서 **+추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f06-122">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="d4f06-123">ID 공급자 구성에 친숙한 **이름** 을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f06-123">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="d4f06-124">예를 들어 "WeChat"을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f06-124">For example, enter "WeChat".</span></span>
5. <span data-ttu-id="d4f06-125">**ID 공급자 형식**을 클릭하고 **WeChat**을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f06-125">Click **Identity provider type**, select **WeChat**, and click **OK**.</span></span>
6. <span data-ttu-id="d4f06-126">**이 ID 공급자 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f06-126">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="d4f06-127">**클라이언트 ID**로 앞에서 복사한 **앱 키**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f06-127">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="d4f06-128">**클라이언트 암호**로 앞에서 복사한 **앱 암호**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f06-128">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="d4f06-129">**확인**을 클릭한 다음 **만들기**를 클릭하여 WeChat 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f06-129">Click **OK** and then click **Create** to save your WeChat configuration.</span></span>

