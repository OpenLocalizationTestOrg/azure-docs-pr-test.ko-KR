---
title: "Azure Active Directory B2C: WeChat 구성 | Microsoft Docs"
description: "등록 및 로그인 tooconsumers WeChat 계정 Azure Active Directory B2C에 의해 보안 되는 응용 프로그램에 제공 합니다."
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
ms.openlocfilehash: 92cc3579d818d2379a503ccc695138b33a34466d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-wechat-accounts"></a><span data-ttu-id="1f528-103">Azure Active Directory B2C: WeChat 계정 등록 및 로그인 tooconsumers 제공</span><span class="sxs-lookup"><span data-stu-id="1f528-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with WeChat accounts</span></span>

> [!NOTE]
> <span data-ttu-id="1f528-104">이 기능은 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="1f528-104">This feature is in preview.</span></span>
> 

## <a name="create-a-wechat-application"></a><span data-ttu-id="1f528-105">WeChat 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="1f528-105">Create a WeChat application</span></span>

<span data-ttu-id="1f528-106">toouse WeChat (Azure AD) Azure Active Directory B2C에을 id 공급자로 toocreate WeChat 응용 프로그램에 필요 하 고이 hello 오른쪽 매개 변수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f528-106">toouse WeChat as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a WeChat application and supply it with hello right parameters.</span></span> <span data-ttu-id="1f528-107">하면 WeChat 계정 toodo이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1f528-107">You need a WeChat account toodo this.</span></span> <span data-ttu-id="1f528-108">없는 경우 모바일 앱 중 하나를 통해 등록하거나 QQ 번호를 사용하여 하나를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f528-108">If you don’t have one, you can get one by signing up through one of their mobile apps or by using your QQ number.</span></span> <span data-ttu-id="1f528-109">그 후에 등록 된 hello WeChat 개발자 프로그램 계정을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1f528-109">After that, get your account registered with hello WeChat developer program.</span></span> <span data-ttu-id="1f528-110">자세한 내용은 [여기](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f528-110">You can find more information [here](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span></span>

### <a name="register-a-wechat-application"></a><span data-ttu-id="1f528-111">WeChat 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="1f528-111">Register a WeChat application</span></span>

1. <span data-ttu-id="1f528-112">너무 이동[https://open.weixin.qq.com/](https://open.weixin.qq.com/) 로그인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="1f528-112">Go too[https://open.weixin.qq.com/](https://open.weixin.qq.com/) and log in.</span></span>
2. <span data-ttu-id="1f528-113">**管理中心**(관리 센터)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f528-113">Click on **管理中心** (management center).</span></span>
3. <span data-ttu-id="1f528-114">Hello 필요한 단계 tooregister 새 응용 프로그램을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1f528-114">Follow hello necessary steps tooregister a new application.</span></span>
4. <span data-ttu-id="1f528-115">**授权回调域**(콜백 URL)에 `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1f528-115">For **授权回调域** (callback URL), enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="1f528-116">예를 들어 경우 프로그램 `tenant_name` contoso.onmicrosoft.com 집합 hello URL toobe은 `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`합니다.</span><span class="sxs-lookup"><span data-stu-id="1f528-116">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
5. <span data-ttu-id="1f528-117">찾기 및 복사 hello **앱 ID** 및 **응용 프로그램 키는**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f528-117">Find and copy hello **APP ID** and **APP KEY**.</span></span> <span data-ttu-id="1f528-118">나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1f528-118">You will need these later.</span></span>

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="1f528-119">테넌트에서 WeChat을 ID 공급자로 구성</span><span class="sxs-lookup"><span data-stu-id="1f528-119">Configure WeChat as an identity provider in your tenant</span></span>
1. <span data-ttu-id="1f528-120">다음 단계를 너무[toohello B2C 기능 블레이드를 탐색](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure 포털에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f528-120">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="1f528-121">Hello B2C 기능 블레이드에서 클릭 **Id 공급자**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f528-121">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="1f528-122">클릭 **+ 추가** hello hello 블레이드 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f528-122">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="1f528-123">친숙 한 제공 **이름** hello id 공급자 구성에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f528-123">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="1f528-124">예를 들어 "WeChat"을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1f528-124">For example, enter "WeChat".</span></span>
5. <span data-ttu-id="1f528-125">**ID 공급자 형식**을 클릭하고 **WeChat**을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f528-125">Click **Identity provider type**, select **WeChat**, and click **OK**.</span></span>
6. <span data-ttu-id="1f528-126">**이 ID 공급자 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f528-126">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="1f528-127">Hello 입력 **응용 프로그램 키는** hello로 앞에서 복사한 **클라이언트 ID**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f528-127">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="1f528-128">Hello 입력 **응용 프로그램 암호** hello로 앞에서 복사한 **클라이언트 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f528-128">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="1f528-129">클릭 **확인** 클릭 하 고 **만들기** toosave WeChat 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f528-129">Click **OK** and then click **Create** toosave your WeChat configuration.</span></span>

