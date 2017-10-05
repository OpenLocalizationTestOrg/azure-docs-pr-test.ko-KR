---
title: "범위 지정 필터를 사용하여 앱 프로비전 | Microsoft Docs"
description: "개체가 비즈니스 요구 사항을 충족하지 못하는 경우 프로비전하는 자동화된 사용자를 지원하는 앱의 개체가 실제로 프로비전되지 않도록 하기 위한 지정 범위 필터 사용 방법을 알아봅니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: bcfbda74-e4d4-4859-83bc-06b104df3918
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 109635052e2ded33831b050eb12d50745944091b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a><span data-ttu-id="6064a-103">범위 지정 필터를 사용한 특성 기반 응용 프로그램 프로비전</span><span class="sxs-lookup"><span data-stu-id="6064a-103">Attribute-based application provisioning with scoping filters</span></span>
<span data-ttu-id="6064a-104">이 섹션의 목적은 범위 지정 필터를 사용하여 어떤 사용자를 응용 프로그램에 프로비전할지 결정하는 특성 기반 규칙을 정의하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6064a-104">The objective of this section is to explain how to use scoping filters to define attribute-based rules that determine which users are provisioned to the application.</span></span>

## <a name="clauses-and-scope-groups"></a><span data-ttu-id="6064a-105">절 및 범위 그룹</span><span class="sxs-lookup"><span data-stu-id="6064a-105">Clauses and Scope Groups</span></span>
![범위 지정 필터][1] 

<span data-ttu-id="6064a-107">범위 지정 필터는 하나 이상의 **그룹 범위**에 의해 정의되며, 각 그룹 범위는 하나 이상의 **절**을 유지하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6064a-107">Scoping filters are defined by one or more **scope groups**, each of which hold one or more **clauses**.</span></span> <span data-ttu-id="6064a-108">특정 범위 그룹에 대한 절을 보려면 그룹 이름의 왼쪽에 있는 화살표를 클릭하여 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="6064a-108">To see the clauses for a particular scope group, expand it by clicking the arrow to the left of the group name.</span></span>

<span data-ttu-id="6064a-109">**절** 은 각 사용자의 특성을 평가하여 어떤 사용자가 범위 지정 필터를 통과할 수 있는지를 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="6064a-109">A **clause** determines which users are allowed to pass through the scoping filter by evaluating each user’s attributes.</span></span> <span data-ttu-id="6064a-110">예를 들어, 사용자의 '상태' 특성이 뉴욕이어야 하는 절을 가졌기 때문에 뉴욕의 사용자만 응용 프로그램에 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="6064a-110">For example, you might have one clause that requires that a user’s ‘state’ attribute equal New York, so only New York users are provisioned into the application.</span></span>

![범위 지정 그룹 이름][2] 

<span data-ttu-id="6064a-112">위의 스크린샷에 나타난 것처럼, 각 **범위 그룹**은 하나의 필수 **절**을 가지고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6064a-112">Each **scope group** starts with one mandatory **clause**, as shown in the screenshot above.</span></span> <span data-ttu-id="6064a-113">이 절은 사용자가 지정 범위 필터에 의해 평가되기 전에 먼저 응용 프로그램에 할당되어있어야 한다는 것을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="6064a-113">This clause simply states that the user must first be assigned to the application before it’s evaluated by your scoping filters.</span></span> <span data-ttu-id="6064a-114">이 절은 삭제하거나 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6064a-114">This clause cannot be deleted or modified.</span></span>

<span data-ttu-id="6064a-115">적절한 단추를 눌러 새 절이나 새 범위 그룹을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6064a-115">You can add new clauses or new scope groups by pressing the appropriate button.</span></span> <span data-ttu-id="6064a-116">**범위 그룹 이름** 속성을 편집하여 각 범위 그룹에 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6064a-116">You can give each scope group a name by editing its **Scope Group Name** property.</span></span>

## <a name="how-scoping-filters-are-evaluated"></a><span data-ttu-id="6064a-117">범위 지정 필터 평가 방법</span><span class="sxs-lookup"><span data-stu-id="6064a-117">How Scoping Filters are Evaluated</span></span>
<span data-ttu-id="6064a-118">프로비전을 하는 동안 모든 할당된 사용자를 범위 지정 필터에 대해 테스트하여 응용 프로그램에 액세스 권한이 있는지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="6064a-118">During provisioning, we test every assigned user against your scoping filters to determine if that user deserves access to the application.</span></span> <span data-ttu-id="6064a-119">사용자가 필터링되지 않기 위해 각 절이 반드시 통과해야 하는 테스트를 받고 있는 것으로 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6064a-119">You can think of each clause as being a test that must be passed in order for the user to avoid getting filtered out.</span></span> 

<span data-ttu-id="6064a-120">지정 범위가 여러 개 정의된 경우, 각 사용자는 응용 프로그램에 액세스하려면 최소 한 개의 지정 범위를 통과해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6064a-120">If you have multiple scope groups defined, each user must pass at least one of them to access the application.</span></span> <span data-ttu-id="6064a-121">그러나 각 범위 그룹 내에서 사용자는 해당 특정 범위 그룹을 통과하는 모든 절을 통과해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6064a-121">Within each scope group, however, the user must pass every clause to pass that specific scope group.</span></span> 

<span data-ttu-id="6064a-122">즉, 범위 그룹이 함께 OR 처리되고 있으며 절들은 함께 AND 처리됨으로써 그 안에 있다고 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6064a-122">In other words, you can think of scope groups as being OR’d together, and you can think of the clauses within them as being AND’d together.</span></span> <span data-ttu-id="6064a-123">예를 들어, 다음의 지정 범위 필터를 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="6064a-123">For example, consider the scoping filter below:</span></span>

![범위 지정 그룹 이름][3]  

<span data-ttu-id="6064a-125">프로비전되는 범위 지정 필터에 따라 사용자는 다음 조건을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6064a-125">According to this scoping filter, users must satisfy the following criteria, to be provisioned:</span></span>

1. <span data-ttu-id="6064a-126">응용 프로그램에 할당되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6064a-126">They must be assigned to the application.</span></span>
2. <span data-ttu-id="6064a-127">엔지니어링 부서에서 근무해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6064a-127">They must work in the Engineering department</span></span>
3. <span data-ttu-id="6064a-128">샌프란시스코 또는 캐나다에서 근무해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6064a-128">They must be work in either San Francisco or Canada.</span></span>

## <a name="related-articles"></a><span data-ttu-id="6064a-129">관련 문서</span><span class="sxs-lookup"><span data-stu-id="6064a-129">Related Articles</span></span>
* [<span data-ttu-id="6064a-130">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="6064a-130">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="6064a-131">SaaS 응용 프로그램에 자동화된 사용자 프로비저닝 및 프로비저닝 해제</span><span class="sxs-lookup"><span data-stu-id="6064a-131">Automate User Provisioning and Deprovisioning to SaaS Applications</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="6064a-132">사용자 프로비저닝에 대한 특성 매핑 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="6064a-132">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="6064a-133">특성 매핑에 대한 식 작성</span><span class="sxs-lookup"><span data-stu-id="6064a-133">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="6064a-134">계정 프로비전 알림</span><span class="sxs-lookup"><span data-stu-id="6064a-134">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="6064a-135">SCIM를 사용하여 Azure Active Directory으로부터 응용 프로그램에 사용자 및 그룹의 자동 프로비전 사용</span><span class="sxs-lookup"><span data-stu-id="6064a-135">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="6064a-136">SaaS App을 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="6064a-136">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
