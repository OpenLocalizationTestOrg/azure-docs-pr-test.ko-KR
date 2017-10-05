---
title: "Azure Active Directory B2C: 사용자 지정 특성 | Microsoft Docs"
description: "Azure Active Directory B2C에서 사용자 지정 특성을 사용하여 소비자에 대한 정보를 수집하는 방법"
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
ms.openlocfilehash: 356aaeff3a78fc7b682d621e8e0de9312582b2fe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-to-collect-information-about-your-consumers"></a><span data-ttu-id="e32e9-103">Azure Active Directory B2C: 사용자 지정 특성을 사용하여 소비자에 대한 정보를 수집</span><span class="sxs-lookup"><span data-stu-id="e32e9-103">Azure Active Directory B2C: Use custom attributes to collect information about your consumers</span></span>
<span data-ttu-id="e32e9-104">Azure Active Directory(Azure AD) B2C 디렉터리에는 지정된 이름, 성, 도시, 우편 번호 등 기본 제공 정보(특성) 집합이 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e32e9-104">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of information (attributes): Given Name, Surname, City, Postal Code, and other attributes.</span></span> <span data-ttu-id="e32e9-105">그러나 모든 소비자 지향 응용 프로그램에는 소비자로부터 수집하려는 정보에 대한 고유한 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e32e9-105">However, every consumer-facing application has unique requirements on what attributes to gather from consumers.</span></span> <span data-ttu-id="e32e9-106">Azure AD B2C를 사용하면 각 소비자 계정에 저장된 특성 집합을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e32e9-106">With Azure AD B2C, you can extend the set of attributes stored on each consumer account.</span></span> <span data-ttu-id="e32e9-107">[Azure 포털](https://portal.azure.com/) 에 사용자 지정 특성을 만들고 아래와 같이 등록 정책에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e32e9-107">You can create custom attributes on the [Azure portal](https://portal.azure.com/) and use it in your sign-up policies, as shown below.</span></span> <span data-ttu-id="e32e9-108">또한 [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md)를 사용하여 이러한 특성을 읽고 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e32e9-108">You can also read and write these attributes by using the [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e32e9-109">사용자 지정 특성은 [Azure AD Graph API 디렉터리 스키마 확장](https://msdn.microsoft.com/library/azure/dn720459.aspx)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e32e9-109">Custom attributes use [Azure AD Graph API Directory Schema Extensions](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span></span>
> 
> 

## <a name="create-a-custom-attribute"></a><span data-ttu-id="e32e9-110">사용자 지정 특성 만들기</span><span class="sxs-lookup"><span data-stu-id="e32e9-110">Create a custom attribute</span></span>
1. <span data-ttu-id="e32e9-111">[다음 단계에 따라 Azure 포털의 B2C 기능 블레이드로 이동합니다](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="e32e9-111">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="e32e9-112">**사용자 특성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e32e9-112">Click **User attributes**.</span></span>
3. <span data-ttu-id="e32e9-113">블레이드의 위쪽에서 **+추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e32e9-113">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="e32e9-114">사용자 지정 특성(예: "ShoeSize")에 **이름**을 제공하고 필요에 따라 **설명**을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e32e9-114">Provide a **Name** for the custom attribute (for example, "ShoeSize") and optionally, a **Description**.</span></span> <span data-ttu-id="e32e9-115">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e32e9-115">Click **Create**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e32e9-116">현재 "문자열" **데이터 형식** 만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e32e9-116">Only the "String" **Data Type** is currently available.</span></span>
   > 
   > 

<span data-ttu-id="e32e9-117">사용자 지정 특성은 **사용자 특성**의 목록 및 등록 정책의 사용에 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="e32e9-117">The custom attribute is now available in the list of **User attributes**, and for use in your sign-up policies.</span></span>

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a><span data-ttu-id="e32e9-118">등록 정책에 사용자 지정 특성 사용</span><span class="sxs-lookup"><span data-stu-id="e32e9-118">Use a custom attribute in your sign-up policy</span></span>
1. <span data-ttu-id="e32e9-119">[다음 단계에 따라 Azure 포털의 B2C 기능 블레이드로 이동합니다](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="e32e9-119">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="e32e9-120">**등록 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e32e9-120">Click **Sign-up policies**.</span></span>
3. <span data-ttu-id="e32e9-121">사용자의 등록 정책(예: "B2C_1_SiUp")을 클릭하여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e32e9-121">Click your sign-up policy (for example, "B2C_1_SiUp") to open it.</span></span> <span data-ttu-id="e32e9-122">블레이드 위쪽에서 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e32e9-122">Click **Edit** at the top of the blade.</span></span>
4. <span data-ttu-id="e32e9-123">**등록 특성**을 클릭하고 사용자 지정 특성을 선택합니다(예: "ShoeSize").</span><span class="sxs-lookup"><span data-stu-id="e32e9-123">Click **Sign-up attributes** and select the custom attribute (for example, "ShoeSize").</span></span> <span data-ttu-id="e32e9-124">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e32e9-124">Click **OK**.</span></span>
5. <span data-ttu-id="e32e9-125">**응용 프로그램 클레임**을 클릭하고 사용자 지정 특성을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e32e9-125">Click **Application claims** and select the custom attribute.</span></span> <span data-ttu-id="e32e9-126">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e32e9-126">Click **OK**.</span></span>
6. <span data-ttu-id="e32e9-127">블레이드 위쪽에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e32e9-127">Click **Save** at the top of the blade.</span></span>

<span data-ttu-id="e32e9-128">정책에서 "지금 실행" 기능을 사용하여 고객 환경을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e32e9-128">You can use the "Run now" feature on the policy to verify the consumer experience.</span></span> <span data-ttu-id="e32e9-129">이제 소비자를 등록하는 동안 수집되는 특성의 목록에서 "ShoeSize"을 표시되고 응용 프로그램으로 다시 전송되는 토큰에 표시되야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e32e9-129">You should now see "ShoeSize" in the list of attributes collected during consumer sign-up, and see it in the token sent back to your application.</span></span>

## <a name="notes"></a><span data-ttu-id="e32e9-130">참고 사항</span><span class="sxs-lookup"><span data-stu-id="e32e9-130">Notes</span></span>
* <span data-ttu-id="e32e9-131">등록 정책과 함께 등록 또는 로그인 정책 및 프로필 편집 정책에서 사용자 지정 특성을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e32e9-131">Along with sign-up policies, custom attributes can also be used in sign-up or sign-in policies and profile editing policies.</span></span>
* <span data-ttu-id="e32e9-132">사용자 지정 특성의 알려진 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e32e9-132">There is a known limitation of custom attributes.</span></span> <span data-ttu-id="e32e9-133">**사용자 특성**목록에 추가될 때가 아니라 정책에 사용하는 경우 처음으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e32e9-133">It is only created the first time it is used in any policy, and not when you add it to the list of **User attributes**.</span></span>

