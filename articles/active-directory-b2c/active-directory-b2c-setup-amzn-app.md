---
title: "Azure Active Directory B2C: Amazon 구성 | Microsoft Docs"
description: "등록 및 로그인 tooconsumers Amazon 계정 Azure Active Directory B2C에 의해 보안 되는 응용 프로그램에 제공 합니다."
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
ms.openlocfilehash: 60d7c4b76d9d3e86ed535765329abed07f1e5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-amazon-accounts"></a><span data-ttu-id="4f4db-103">Azure Active Directory B2C: Amazon 계정 등록 및 로그인 tooconsumers 제공</span><span class="sxs-lookup"><span data-stu-id="4f4db-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Amazon accounts</span></span>
## <a name="create-an-amazon-application"></a><span data-ttu-id="4f4db-104">Amazon 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="4f4db-104">Create an Amazon application</span></span>
<span data-ttu-id="4f4db-105">Amazon toouse (Azure AD) Azure Active Directory B2C에을 id 공급자로 toocreate Amazon 응용 프로그램에 필요 하 고이 hello 오른쪽 매개 변수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-105">toouse Amazon as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate an Amazon application and supply it with hello right parameters.</span></span> <span data-ttu-id="4f4db-106">하면 Amazon 계정 toodo이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-106">You need an Amazon account toodo this.</span></span> <span data-ttu-id="4f4db-107">계정이 없는 경우 [http://www.amazon.com/](http://www.amazon.com/)에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-107">If you don’t have one, you can get it at [http://www.amazon.com/](http://www.amazon.com/).</span></span>

1. <span data-ttu-id="4f4db-108">Toohello 이동 [Amazon Developer Center](https://login.amazon.com/) Amazon 계정 자격 증명으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-108">Go toohello [Amazon Developer Center](https://login.amazon.com/) and sign in with your Amazon account credentials.</span></span>
2. <span data-ttu-id="4f4db-109">이미 수행 하는 경우 클릭 **등록**hello 개발자 등록 단계를 수행 하 고 hello 방침에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-109">If you have not already done so, click **Sign Up**, follow hello developer registration steps, and accept hello policy.</span></span>
3. <span data-ttu-id="4f4db-110">**새 응용 프로그램 등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-110">Click **Register new application**.</span></span>
   
    ![Hello Amazon 웹 사이트에서 새 응용 프로그램 등록](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. <span data-ttu-id="4f4db-112">응용 프로그램 정보(**이름**, **설명** 및 **개인 정보 알림 URL**)를 제공하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-112">Provide application information (**Name**, **Description**, and **Privacy Notice URL**) and click **Save**.</span></span>
   
    ![Amazon에 새 응용 프로그램을 등록하기 위한 응용 프로그램 정보 제공](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. <span data-ttu-id="4f4db-114">Hello에 **웹 설정** 섹션의 hello 값 복사 **클라이언트 ID** 및 **클라이언트 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-114">In hello **Web Settings** section, copy hello values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="4f4db-115">(Tooclick hello 필요한 **암호 표시** toosee 단추입니다.) 둘 다 필요 tooconfigure 테 넌 트를 id 공급자로 Amazon 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-115">(You need tooclick hello **Show Secret** button toosee this.) You need both of them tooconfigure Amazon as an identity provider in your tenant.</span></span> <span data-ttu-id="4f4db-116">클릭 **편집** hello hello 섹션 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-116">Click **Edit** at hello bottom of hello section.</span></span> <span data-ttu-id="4f4db-117">**클라이언트 암호** 는 중요한 보안 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-117">**Client Secret** is an important security credential.</span></span>
   
    ![Amazon에 새 응용 프로그램에 대한 클라이언트 ID 및 클라이언트 암호 제공](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. <span data-ttu-id="4f4db-119">입력 `https://login.microsoftonline.com` hello에 **허용 자바 스크립트 원본** 필드 및 `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` hello에 **반환 Url 허용** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-119">Enter `https://login.microsoftonline.com` in hello **Allowed JavaScript Origins** field and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Allowed Return URLs** field.</span></span> <span data-ttu-id="4f4db-120">**{tenant}** 를 사용자의 테넌트 이름(예: contoso.onmicrosoft.com)으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-120">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="4f4db-121">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-121">Click **Save**.</span></span> <span data-ttu-id="4f4db-122">hello **{tenant}** 값은 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-122">hello **{tenant}** value is case-sensitive.</span></span>
   
    ![Amazon에 새 응용 프로그램에 대한 JavaScript 원본 및 반환 URL 제공](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="4f4db-124">테넌트에서 Amazon을 ID 공급자로 구성</span><span class="sxs-lookup"><span data-stu-id="4f4db-124">Configure Amazon as an identity provider in your tenant</span></span>
1. <span data-ttu-id="4f4db-125">다음 단계를 너무[toohello B2C 기능 블레이드를 탐색](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure 포털에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-125">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="4f4db-126">Hello B2C 기능 블레이드에서 클릭 **Id 공급자**합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-126">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="4f4db-127">클릭 **+ 추가** hello hello 블레이드 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-127">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="4f4db-128">친숙 한 제공 **이름** hello id 공급자 구성에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-128">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="4f4db-129">예를 들어 "Amzn"을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-129">For example, enter "Amzn".</span></span>
5. <span data-ttu-id="4f4db-130">**ID 공급자 형식**을 클릭하고 **Amazon**을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-130">Click **Identity provider type**, select **Amazon**, and click **OK**.</span></span>
6. <span data-ttu-id="4f4db-131">클릭 **이 id 공급자 설정** hello 앞에서 만든 Amazon 응용 프로그램의 hello 클라이언트 ID와 클라이언트 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-131">Click **Set up this identity provider** and enter hello client ID and client secret of hello Amazon application that you created earlier.</span></span>
7. <span data-ttu-id="4f4db-132">클릭 **확인** 클릭 하 고 **만들기** toosave Amazon 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-132">Click **OK** and then click **Create** toosave your Amazon configuration.</span></span>

