---
title: "Azure Active Directory B2C: Twitter 구성 | Microsoft 문서"
description: "Twitter 계정에 Azure Active Directory B2C에 의해 보안 되는 응용 프로그램 등록 및 로그인 tooconsumers를 제공 합니다."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 579a6841-9329-45b8-a351-da4315a6634e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/06/2017
ms.author: parakhj
ms.openlocfilehash: 275c5c73fd5e8e5075e77fee942cbc1b5e1586cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-twitter-accounts"></a><span data-ttu-id="ce299-103">Azure Active Directory B2C: Twitter 계정 등록 및 로그인 tooconsumers 제공</span><span class="sxs-lookup"><span data-stu-id="ce299-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Twitter accounts</span></span>

> [!NOTE]
> <span data-ttu-id="ce299-104">이 기능은 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ce299-104">This feature is in preview.</span></span>
> 

## <a name="create-a-twitter-application"></a><span data-ttu-id="ce299-105">Twitter 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="ce299-105">Create a Twitter application</span></span>
<span data-ttu-id="ce299-106">toouse는 toocreate Twitter 응용 프로그램에 필요 하 고 hello 오른쪽 매개 변수를 제공 (Azure AD) Azure Active Directory B2C에 대 한 id 공급자로 Twitter입니다.</span><span class="sxs-lookup"><span data-stu-id="ce299-106">toouse Twitter as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Twitter application and supply it with hello right parameters.</span></span> <span data-ttu-id="ce299-107">하면 Twitter 개발자 계정 toodo이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ce299-107">You need a Twitter developer account toodo this.</span></span> <span data-ttu-id="ce299-108">계정이 없는 경우 [https://dev.twitter.com/](https://dev.twitter.com/)에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce299-108">If you don’t have one, you can get it at [https://dev.twitter.com/](https://dev.twitter.com/).</span></span>

1. <span data-ttu-id="ce299-109">Toohello 이동 [개발자의 웹 사이트를 Twitter](https://dev.twitter.com/) 및 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce299-109">Go toohello [Twitter developer's website](https://dev.twitter.com/) and sign in with your credentials.</span></span>
2. <span data-ttu-id="ce299-110">**Tools & Support**(도구 및 지원)에서 **My apps**(내 앱)를 클릭하고 **Create New App**(새 앱 만들기)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce299-110">Click **My apps** under **Tools & Support** and then click **Create New App**.</span></span> 
3. <span data-ttu-id="ce299-111">Hello 형태로 hello에 대 한 값을 제공 **이름**, **설명**, 및 **웹 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="ce299-111">In hello form, provide a value for hello **Name**, **Description**, and **Website**.</span></span>
4. <span data-ttu-id="ce299-112">Hello에 대 한 **콜백 URL**, 입력 `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`합니다.</span><span class="sxs-lookup"><span data-stu-id="ce299-112">For hello **Callback URL**, enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span></span> <span data-ttu-id="ce299-113">있는지 tooreplace 확인 **{tenant}** 테 넌 트의 이름 (예를 들어 contosob2c.onmicrosoft.com)으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce299-113">Make sure tooreplace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
5. <span data-ttu-id="ce299-114">Hello 상자 tooagree toohello 확인 **개발자 계약** 클릭 **Twitter 응용 프로그램을 만드는**합니다.</span><span class="sxs-lookup"><span data-stu-id="ce299-114">Check hello box tooagree toohello **Developer Agreement** and click **Create your Twitter application**.</span></span>
6. <span data-ttu-id="ce299-115">Hello 응용 프로그램을 만든 후 클릭 **키와 액세스 토큰이**합니다.</span><span class="sxs-lookup"><span data-stu-id="ce299-115">Once hello app is created, click **Keys and Access Tokens**.</span></span>
7. <span data-ttu-id="ce299-116">hello 값을 복사 **소비자 키** 및 **소비자 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="ce299-116">Copy hello value of **Consumer Key** and **Consumer Secret**.</span></span> <span data-ttu-id="ce299-117">둘 모두 필요 합니다 tooconfigure Twitter id 공급자로 테 넌 트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce299-117">You will need both of them tooconfigure Twitter as an identity provider in your tenant.</span></span>

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="ce299-118">테넌트에서 Twitter를 ID 공급자로 구성</span><span class="sxs-lookup"><span data-stu-id="ce299-118">Configure Twitter as an identity provider in your tenant</span></span>
1. <span data-ttu-id="ce299-119">다음 단계를 너무[toohello B2C 기능 블레이드를 탐색](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure 포털에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce299-119">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="ce299-120">Hello B2C 기능 블레이드에서 클릭 **Id 공급자**합니다.</span><span class="sxs-lookup"><span data-stu-id="ce299-120">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="ce299-121">클릭 **+ 추가** hello hello 블레이드 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce299-121">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="ce299-122">친숙 한 제공 **이름** hello id 공급자 구성에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce299-122">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="ce299-123">예를 들어 "Twitter"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ce299-123">For example, enter "Twitter".</span></span>
5. <span data-ttu-id="ce299-124">**ID 공급자 형식**을 클릭하고 **Twitter**를 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce299-124">Click **Identity provider type**, select **Twitter**, and click **OK**.</span></span>
6. <span data-ttu-id="ce299-125">클릭 **이 id 공급자 설정** hello Twitter 입력 **소비자 키** hello에 대 한 **클라이언트 id** Twitter hello 및 **소비자 암호**hello에 대 한 **클라이언트 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="ce299-125">Click **Set up this identity provider** and enter hello Twitter **Consumer Key** for hello **Client id** and hello Twitter **Consumer Secret** for hello **Client secret**.</span></span>
7. <span data-ttu-id="ce299-126">클릭 **확인**, 클릭 하 고 **만들기** toosave Twitter 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce299-126">Click **OK**, and then click **Create** toosave your Twitter configuration.</span></span>

