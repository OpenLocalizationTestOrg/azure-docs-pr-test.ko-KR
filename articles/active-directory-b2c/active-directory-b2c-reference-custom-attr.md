---
title: "Azure Active Directory B2C: 사용자 지정 특성 | Microsoft Docs"
description: "소비자에 대 한 Azure Active Directory B2C toocollect 정보에 toouse 사용자 지정 특성 하는 방법"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 055ffb0a-197b-4716-8dad-1fd8a01e174f
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: fb1bff77ad54c246c6d2f69f39c03eafb76fe6bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-toocollect-information-about-your-consumers"></a><span data-ttu-id="3b022-103">Azure Active Directory B2C: 소비자에 대 한 사용자 지정 특성 toocollect 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-103">Azure Active Directory B2C: Use custom attributes toocollect information about your consumers</span></span>
<span data-ttu-id="3b022-104">Azure Active Directory(Azure AD) B2C 디렉터리에는 지정된 이름, 성, 도시, 우편 번호 등 기본 제공 정보(특성) 집합이 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-104">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of information (attributes): Given Name, Surname, City, Postal Code, and other attributes.</span></span> <span data-ttu-id="3b022-105">그러나 모든 소비자 용 응용 프로그램에 어떤 특성 toogather는 소비자에 고유한 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-105">However, every consumer-facing application has unique requirements on what attributes toogather from consumers.</span></span> <span data-ttu-id="3b022-106">Azure AD B2C hello 각 소비자 계정에 저장 하는 특성 집합을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-106">With Azure AD B2C, you can extend hello set of attributes stored on each consumer account.</span></span> <span data-ttu-id="3b022-107">Hello에 사용자 지정 특성을 만들 수 있습니다 [Azure 포털](https://portal.azure.com/) 아래와 같이 등록 정책에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-107">You can create custom attributes on hello [Azure portal](https://portal.azure.com/) and use it in your sign-up policies, as shown below.</span></span> <span data-ttu-id="3b022-108">또한 읽고 수 hello를 사용 하 여 이러한 특성을 쓸 [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-108">You can also read and write these attributes by using hello [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3b022-109">사용자 지정 특성은 [Azure AD Graph API 디렉터리 스키마 확장](https://msdn.microsoft.com/library/azure/dn720459.aspx)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-109">Custom attributes use [Azure AD Graph API Directory Schema Extensions](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span></span>
> 
> 

## <a name="create-a-custom-attribute"></a><span data-ttu-id="3b022-110">사용자 지정 특성 만들기</span><span class="sxs-lookup"><span data-stu-id="3b022-110">Create a custom attribute</span></span>
1. <span data-ttu-id="3b022-111">[이러한 단계 toonavigate toohello B2C 기능 블레이드 hello Azure 포털에 따라](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)합니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-111">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="3b022-112">**사용자 특성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-112">Click **User attributes**.</span></span>
3. <span data-ttu-id="3b022-113">클릭 **+ 추가** hello hello 블레이드 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-113">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="3b022-114">제공 된 **이름** hello 사용자 지정 특성 (예: "ShoeSize") 및 필요에 따라는 **설명**합니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-114">Provide a **Name** for hello custom attribute (for example, "ShoeSize") and optionally, a **Description**.</span></span> <span data-ttu-id="3b022-115">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-115">Click **Create**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3b022-116">만 "문자열" hello **데이터 형식** 를 현재 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-116">Only hello "String" **Data Type** is currently available.</span></span>
   > 
   > 

<span data-ttu-id="3b022-117">hello 사용자 지정 특성은 현재 hello 목록이 **사용자 특성**, 되며 등록 정책에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-117">hello custom attribute is now available in hello list of **User attributes**, and for use in your sign-up policies.</span></span>

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a><span data-ttu-id="3b022-118">등록 정책에 사용자 지정 특성 사용</span><span class="sxs-lookup"><span data-stu-id="3b022-118">Use a custom attribute in your sign-up policy</span></span>
1. <span data-ttu-id="3b022-119">[이러한 단계 toonavigate toohello B2C 기능 블레이드 hello Azure 포털에 따라](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)합니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-119">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="3b022-120">**등록 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-120">Click **Sign-up policies**.</span></span>
3. <span data-ttu-id="3b022-121">등록 정책 (예: "B2C_1_SiUp") tooopen 클릭 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-121">Click your sign-up policy (for example, "B2C_1_SiUp") tooopen it.</span></span> <span data-ttu-id="3b022-122">클릭 **편집** hello hello 블레이드 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-122">Click **Edit** at hello top of hello blade.</span></span>
4. <span data-ttu-id="3b022-123">클릭 **등록 특성** 및 선택 hello 사용자 지정 특성 (예: "ShoeSize").</span><span class="sxs-lookup"><span data-stu-id="3b022-123">Click **Sign-up attributes** and select hello custom attribute (for example, "ShoeSize").</span></span> <span data-ttu-id="3b022-124">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-124">Click **OK**.</span></span>
5. <span data-ttu-id="3b022-125">클릭 **응용 프로그램 클레임** 및 선택 hello 사용자 지정 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-125">Click **Application claims** and select hello custom attribute.</span></span> <span data-ttu-id="3b022-126">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-126">Click **OK**.</span></span>
6. <span data-ttu-id="3b022-127">클릭 **저장** hello hello 블레이드 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-127">Click **Save** at hello top of hello blade.</span></span>

<span data-ttu-id="3b022-128">Hello 정책 tooverify hello 소비자 경험에 hello "지금 실행" 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-128">You can use hello "Run now" feature on hello policy tooverify hello consumer experience.</span></span> <span data-ttu-id="3b022-129">이제 "ShoeSize" 소비자를 등록 하는 동안 수집 된 특성의 hello 목록에서 참조 하 고 hello 토큰 보낸된 백 tooyour 응용 프로그램에서 참조 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-129">You should now see "ShoeSize" in hello list of attributes collected during consumer sign-up, and see it in hello token sent back tooyour application.</span></span>

## <a name="notes"></a><span data-ttu-id="3b022-130">참고 사항</span><span class="sxs-lookup"><span data-stu-id="3b022-130">Notes</span></span>
* <span data-ttu-id="3b022-131">등록 정책과 함께 등록 또는 로그인 정책 및 프로필 편집 정책에서 사용자 지정 특성을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-131">Along with sign-up policies, custom attributes can also be used in sign-up or sign-in policies and profile editing policies.</span></span>
* <span data-ttu-id="3b022-132">사용자 지정 특성의 알려진 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-132">There is a known limitation of custom attributes.</span></span> <span data-ttu-id="3b022-133">Hello 처음으로 사용 되는 정책에서 만든 에게만 고 toohello 목록을 추가할 때가 아니라 **사용자 특성**합니다.</span><span class="sxs-lookup"><span data-stu-id="3b022-133">It is only created hello first time it is used in any policy, and not when you add it toohello list of **User attributes**.</span></span>

