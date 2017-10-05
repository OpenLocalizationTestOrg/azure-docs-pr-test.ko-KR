---
title: "Azure Active Directory B2C: Twitter 구성 | Microsoft 문서"
description: "소비자에게 Azure Active Directory B2C를 사용하여 보안이 유지되는 응용 프로그램에서 Twitter 계정으로 등록 및 로그인을 제공합니다."
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
ms.openlocfilehash: 82a001dd53cdddcf3b360090f3250af593c96fbb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-twitter-accounts"></a><span data-ttu-id="6e501-103">Azure Active Directory B2C: 고객에게 Twitter 계정으로 등록 및 로그인 제공</span><span class="sxs-lookup"><span data-stu-id="6e501-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Twitter accounts</span></span>

> [!NOTE]
> <span data-ttu-id="6e501-104">이 기능은 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e501-104">This feature is in preview.</span></span>
> 

## <a name="create-a-twitter-application"></a><span data-ttu-id="6e501-105">Twitter 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="6e501-105">Create a Twitter application</span></span>
<span data-ttu-id="6e501-106">Azure AD(Azure Active Directory) B2C에서 Twitter를 ID 공급자로 사용하려면 Twitter 응용 프로그램을 만들고 올바른 매개 변수를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e501-106">To use Twitter as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Twitter application and supply it with the right parameters.</span></span> <span data-ttu-id="6e501-107">이렇게 하려면 Twitter 개발자 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6e501-107">You need a Twitter developer account to do this.</span></span> <span data-ttu-id="6e501-108">계정이 없는 경우 [https://dev.twitter.com/](https://dev.twitter.com/)에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e501-108">If you don’t have one, you can get it at [https://dev.twitter.com/](https://dev.twitter.com/).</span></span>

1. <span data-ttu-id="6e501-109">[Twitter developer's website](https://dev.twitter.com/)(Twitter 개발자 웹 사이트)로 이동하고 사용자 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6e501-109">Go to the [Twitter developer's website](https://dev.twitter.com/) and sign in with your credentials.</span></span>
2. <span data-ttu-id="6e501-110">**Tools & Support**(도구 및 지원)에서 **My apps**(내 앱)를 클릭하고 **Create New App**(새 앱 만들기)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e501-110">Click **My apps** under **Tools & Support** and then click **Create New App**.</span></span> 
3. <span data-ttu-id="6e501-111">폼에서 **Name**(이름), **Description**(설명) 및 **Website**(웹 사이트)의 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6e501-111">In the form, provide a value for the **Name**, **Description**, and **Website**.</span></span>
4. <span data-ttu-id="6e501-112">**Callback URL**(콜백 URL)에 `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6e501-112">For the **Callback URL**, enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span></span> <span data-ttu-id="6e501-113">**{tenant}**를 테넌트의 이름(예: contosob2c.onmicrosoft.com)으로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e501-113">Make sure to replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
5. <span data-ttu-id="6e501-114">상자를 선택하여 **Developer Agreement**(개발자 계약)에 동의하고 **Create your Twitter application**(Twitter 응용 프로그램 만들기)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e501-114">Check the box to agree to the **Developer Agreement** and click **Create your Twitter application**.</span></span>
6. <span data-ttu-id="6e501-115">앱이 만들어지면 **Keys and Access Tokens**(키 및 액세스 토큰) 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e501-115">Once the app is created, click **Keys and Access Tokens**.</span></span>
7. <span data-ttu-id="6e501-116">**Consumer Key**(소비자 키) 및 **Consumer Secret**(소비자 암호)의 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6e501-116">Copy the value of **Consumer Key** and **Consumer Secret**.</span></span> <span data-ttu-id="6e501-117">테넌트에서 Twitter를 ID 공급자로 구성하려면 둘 모두가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6e501-117">You will need both of them to configure Twitter as an identity provider in your tenant.</span></span>

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="6e501-118">테넌트에서 Twitter를 ID 공급자로 구성</span><span class="sxs-lookup"><span data-stu-id="6e501-118">Configure Twitter as an identity provider in your tenant</span></span>
1. <span data-ttu-id="6e501-119">다음 단계에 따라 [Azure 포털의 B2C 기능 블레이드로 이동합니다](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) .</span><span class="sxs-lookup"><span data-stu-id="6e501-119">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="6e501-120">B2C 기능 블레이드에서 **ID 공급자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e501-120">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="6e501-121">블레이드의 위쪽에서 **+추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e501-121">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="6e501-122">ID 공급자 구성에 친숙한 **이름** 을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6e501-122">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="6e501-123">예를 들어 "Twitter"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6e501-123">For example, enter "Twitter".</span></span>
5. <span data-ttu-id="6e501-124">**ID 공급자 형식**을 클릭하고 **Twitter**를 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e501-124">Click **Identity provider type**, select **Twitter**, and click **OK**.</span></span>
6. <span data-ttu-id="6e501-125">**이 ID 공급자 설정**을 클릭하고 **클라이언트 ID**에 Twitter **Consumer Key**(소비자 키)를 입력하고 **클라이언트 암호**에 Twitter **Consumer Secret**(소비자 암호)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6e501-125">Click **Set up this identity provider** and enter the Twitter **Consumer Key** for the **Client id** and the Twitter **Consumer Secret** for the **Client secret**.</span></span>
7. <span data-ttu-id="6e501-126">**확인**을 클릭한 다음 **만들기**를 클릭하여 Twitter 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6e501-126">Click **OK**, and then click **Create** to save your Twitter configuration.</span></span>

