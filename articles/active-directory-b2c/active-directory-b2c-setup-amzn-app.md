---
title: "Azure Active Directory B2C: Amazon 구성 | Microsoft Docs"
description: "소비자에게 Azure Active Directory B2C를 사용하여 보안이 유지되는 응용 프로그램에서 Amazon 계정으로 등록 및 로그인을 제공합니다."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 77c099bb-a005-4d75-87f9-f61e3de48725
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: dcc97e1b7f6287bd7692c52bf068950065a26572
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-amazon-accounts"></a><span data-ttu-id="b6b06-103">Azure Active Directory B2C: 고객에게 Amazon 계정으로 등록 및 로그인 제공</span><span class="sxs-lookup"><span data-stu-id="b6b06-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Amazon accounts</span></span>
## <a name="create-an-amazon-application"></a><span data-ttu-id="b6b06-104">Amazon 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="b6b06-104">Create an Amazon application</span></span>
<span data-ttu-id="b6b06-105">Azure Active Directory(Azure AD) B2C에서 Amazon을 ID 공급자로 사용하려면 먼저 Amazon 응용 프로그램을 만들고 올바른 매개 변수를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6b06-105">To use Amazon as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an Amazon application and supply it with the right parameters.</span></span> <span data-ttu-id="b6b06-106">이 작업을 수행하려면 Amazon 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b6b06-106">You need an Amazon account to do this.</span></span> <span data-ttu-id="b6b06-107">계정이 없는 경우 [http://www.amazon.com/](http://www.amazon.com/)에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6b06-107">If you don’t have one, you can get it at [http://www.amazon.com/](http://www.amazon.com/).</span></span>

1. <span data-ttu-id="b6b06-108">[Amazon 개발자 센터](https://login.amazon.com/) 로 이동하여 Amazon 계정 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b6b06-108">Go to the [Amazon Developer Center](https://login.amazon.com/) and sign in with your Amazon account credentials.</span></span>
2. <span data-ttu-id="b6b06-109">이미 수행한 경우 **등록**을 클릭하고 개발자 등록 단계를 수행하며 정책에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="b6b06-109">If you have not already done so, click **Sign Up**, follow the developer registration steps, and accept the policy.</span></span>
3. <span data-ttu-id="b6b06-110">**새 응용 프로그램 등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6b06-110">Click **Register new application**.</span></span>
   
    ![Amazon 웹 사이트에서 새 응용 프로그램 등록](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. <span data-ttu-id="b6b06-112">응용 프로그램 정보(**이름**, **설명** 및 **개인 정보 알림 URL**)를 제공하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6b06-112">Provide application information (**Name**, **Description**, and **Privacy Notice URL**) and click **Save**.</span></span>
   
    ![Amazon에 새 응용 프로그램을 등록하기 위한 응용 프로그램 정보 제공](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. <span data-ttu-id="b6b06-114">**웹 설정** 섹션에서 **클라이언트 ID** 및 **클라이언트 비밀** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b6b06-114">In the **Web Settings** section, copy the values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="b6b06-115">(이 정보를 보려면 **비밀 표시** 단추를 클릭해야 합니다.) 테넌트에서 Amazon을 ID 공급자로 구성하려면 둘 다 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b6b06-115">(You need to click the **Show Secret** button to see this.) You need both of them to configure Amazon as an identity provider in your tenant.</span></span> <span data-ttu-id="b6b06-116">섹션 아래쪽에서 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6b06-116">Click **Edit** at the bottom of the section.</span></span> <span data-ttu-id="b6b06-117">**클라이언트 암호** 는 중요한 보안 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="b6b06-117">**Client Secret** is an important security credential.</span></span>
   
    ![Amazon에 새 응용 프로그램에 대한 클라이언트 ID 및 클라이언트 암호 제공](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. <span data-ttu-id="b6b06-119">**허용되는 JavaScript 원본** 필드에 `https://login.microsoftonline.com`을 입력하고 **허용되는 반환 URL** 필드에 `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b6b06-119">Enter `https://login.microsoftonline.com` in the **Allowed JavaScript Origins** field and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Allowed Return URLs** field.</span></span> <span data-ttu-id="b6b06-120">**{tenant}** 를 사용자의 테넌트 이름(예: contoso.onmicrosoft.com)으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b6b06-120">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="b6b06-121">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6b06-121">Click **Save**.</span></span> <span data-ttu-id="b6b06-122">**{tenant}** 값은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="b6b06-122">The **{tenant}** value is case-sensitive.</span></span>
   
    ![Amazon에 새 응용 프로그램에 대한 JavaScript 원본 및 반환 URL 제공](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="b6b06-124">테넌트에서 Amazon을 ID 공급자로 구성</span><span class="sxs-lookup"><span data-stu-id="b6b06-124">Configure Amazon as an identity provider in your tenant</span></span>
1. <span data-ttu-id="b6b06-125">다음 단계에 따라 [Azure 포털의 B2C 기능 블레이드로 이동합니다](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) .</span><span class="sxs-lookup"><span data-stu-id="b6b06-125">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="b6b06-126">B2C 기능 블레이드에서 **ID 공급자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6b06-126">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="b6b06-127">블레이드의 위쪽에서 **+추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6b06-127">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="b6b06-128">ID 공급자 구성에 친숙한 **이름** 을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b6b06-128">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="b6b06-129">예를 들어 "Amzn"을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b6b06-129">For example, enter "Amzn".</span></span>
5. <span data-ttu-id="b6b06-130">**ID 공급자 형식**을 클릭하고 **Amazon**을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6b06-130">Click **Identity provider type**, select **Amazon**, and click **OK**.</span></span>
6. <span data-ttu-id="b6b06-131">**이 ID 공급자 설정**을 클릭하고 이전에 만든 Amazon 응용 프로그램의 클라이언트 ID 및 클라이언트 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b6b06-131">Click **Set up this identity provider** and enter the client ID and client secret of the Amazon application that you created earlier.</span></span>
7. <span data-ttu-id="b6b06-132">**확인**, **만들기**를 차례로 클릭하여 Amazon 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b6b06-132">Click **OK** and then click **Create** to save your Amazon configuration.</span></span>

