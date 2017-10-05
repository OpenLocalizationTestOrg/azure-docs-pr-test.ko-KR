---
title: "Azure Active Directory B2C: 셀프 서비스 암호 재설정 | Microsoft Docs"
description: "Azure Active Directory B2C 미리 보기에서 소비자를 위해 셀프 서비스 암호 재설정을 설정하는 방법을 보여주는 항목"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: curtand
ms.assetid: c87ed86e-1520-42b1-8c31-46cd44ed5310
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 0508868e3b00c5771cc26038a3dd71fde6625a84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a><span data-ttu-id="b6f2c-103">Azure Active Directory B2C: 소비자를 위해 셀프 서비스 암호 재설정 설정</span><span class="sxs-lookup"><span data-stu-id="b6f2c-103">Azure Active Directory B2C: Set up self-service password reset for your consumers</span></span>
<span data-ttu-id="b6f2c-104">셀프 서비스 암호 재설정 기능을 사용하면 (로컬 계정에 등록된)소비자는 자체적으로 암호를 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2c-104">With the self-service password reset feature, your consumers (who have signed up for local accounts) can reset their passwords on their own.</span></span> <span data-ttu-id="b6f2c-105">특히 정기적으로 응용 프로그램을 사용하는 수 백만 명의 소비자가 있는 경우 지원 담당자의 부담을 크게 줄여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2c-105">This significantly reduces the burden on your support staff, especially if your application has millions of consumers using it on a regular basis.</span></span> <span data-ttu-id="b6f2c-106">현재 검증된 전자 메일 주소를 지원 복구 방법으로 사용하여 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2c-106">Currently, we only support using a verified email address as a recovery method.</span></span> <span data-ttu-id="b6f2c-107">추가 복구 방법을 나중에 추가합니다.(확인된 전화번호, 보안 질문 등)</span><span class="sxs-lookup"><span data-stu-id="b6f2c-107">We will add additional recovery methods (verified phone number, security questions, etc.) in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="b6f2c-108">이 문서는 로그인 정책의 컨텍스트에서 사용되는 셀프 서비스 암호 재설정에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2c-108">This article applies to self-service password reset used in the context of a sign-in policy.</span></span> <span data-ttu-id="b6f2c-109">완전히 사용자 지정 가능한 암호 재설정 정책이 앱에서 호출되어야 하는 경우 [이 문서](active-directory-b2c-reference-policies.md#create-a-password-reset-policy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2c-109">If you need fully customizable password reset policies invoked from your app, see [this article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span></span>
> 
> 

<span data-ttu-id="b6f2c-110">기본적으로 디렉터리는 셀프 서비스 암호 재설정을 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2c-110">By default, your directory will not have self-service password reset turned on.</span></span> <span data-ttu-id="b6f2c-111">설정하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2c-111">Use the following steps to turn it on:</span></span>

1. <span data-ttu-id="b6f2c-112">[Azure 클래식 포털](https://manage.windowsazure.com/) 에 구독 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2c-112">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) as the Subscription Administrator.</span></span> <span data-ttu-id="b6f2c-113">이는 동일한 직장이나 학교 계정 또는 디렉터리를 만드는 데 사용한 동일한 Microsoft 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2c-113">This is the same work or school account or the same Microsoft account that you used to create your directory.</span></span>
2. <span data-ttu-id="b6f2c-114">왼쪽의 탐색 모음에서 Active Directory 확장으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2c-114">Navigate to the Active Directory extension on the navigation bar on the left side.</span></span>
3. <span data-ttu-id="b6f2c-115">**디렉터리** 탭에서 디렉터리를 찾고 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2c-115">Find your directory under the **Directory** tab and click it.</span></span>
4. <span data-ttu-id="b6f2c-116">**구성** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2c-116">Click the **Configure** tab.</span></span>
5. <span data-ttu-id="b6f2c-117">**사용자 암호 재설정 정책** 섹션으로 스크롤하여 **사용자 암호 재설정 활성화됨** 옵션을 **예**로 토글합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2c-117">Scroll down to the **User password reset policy** section and toggle the **Users enabled for password reset** option to **YES**.</span></span> <span data-ttu-id="b6f2c-118">**대체 메일 주소** 옵션을 선택하고 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2c-118">Notice that the **Alternate Email Address** option is checked; leave it as it is.</span></span>
   
    ![셀프 서비스 암호 재설정](./media/active-directory-b2c-reference-sspr/sspr.png)
6. <span data-ttu-id="b6f2c-120">페이지 맨 아래에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2c-120">Click **Save** at the bottom of the page.</span></span> <span data-ttu-id="b6f2c-121">완료되었습니다!</span><span class="sxs-lookup"><span data-stu-id="b6f2c-121">You're done!</span></span>

<span data-ttu-id="b6f2c-122">테스트하려면 (로컬 계정을 ID 공급자로 가진)로그인 정책에서 "지금 실행" 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2c-122">To test, use the "Run now" feature on any sign-in policy that has local accounts as an identity provider.</span></span> <span data-ttu-id="b6f2c-123">메일 주소 및 암호 또는 사용자 이름 및 암호를 입력하는 로컬 계정 로그인 페이지에서 **계정에 액세스할 수 없나요?** 를 클릭하여 소비자 환경을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2c-123">On the local account sign-in page (where you enter an email address and password, or a username and password), click **Can't access your account?** to verify the consumer experience.</span></span>

> [!NOTE]
> <span data-ttu-id="b6f2c-124">셀프 서비스 암호 재설정 페이지는 [회사 브랜딩 기능](../active-directory/active-directory-add-company-branding.md)을 사용하여 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2c-124">The self-service password reset pages can be customized by using the [company branding feature](../active-directory/active-directory-add-company-branding.md).</span></span>
> 
> 

