---
title: "리소스 정책에 대 한 aaaAzure 포털 | Microsoft Docs"
description: "설명 방법을 toouse 포털 toocreate Azure 리소스 관리자 정책 및 관리 합니다. Hello 구독 또는 리소스 그룹에 정책은 적용할 수 있습니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: tomfitz
ms.openlocfilehash: ce6413386317e532b63761a24458b85c996af4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-tooassign-and-manage-resource-policies"></a><span data-ttu-id="10822-104">Azure 포털 tooassign를 사용 하 고 리소스 정책 관리</span><span class="sxs-lookup"><span data-stu-id="10822-104">Use Azure portal tooassign and manage resource policies</span></span>
<span data-ttu-id="10822-105">Azure 포털 hello 있습니다 tooassign 리소스 tooresource 그룹 정책 및 구독을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="10822-105">hello Azure portal enables you tooassign resource policies tooresource groups and subscriptions.</span></span> <span data-ttu-id="10822-106">hello 사용자 인터페이스를 사용 하면 쉽게 tooselect hello 정책 tooassign, 원하고 해당 정책 toocustomize hello 정책 설정에 대 한 매개 변수 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="10822-106">hello user interface makes it easy tooselect hello policy that you want tooassign, and specify parameter values for that policy toocustomize hello policy settings.</span></span> 

<span data-ttu-id="10822-107">tooassign hello 포털을 통해 정책으로는 hello 정책 정의 구독에 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10822-107">tooassign a policy through hello portal, hello policy definition must already exist in your subscription.</span></span> <span data-ttu-id="10822-108">사용자 구독에는 몇 가지 기본 제공 정책 정의 하면 tooassign tooresource 그룹 또는 구독에 대해 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="10822-108">Your subscription has several built-in policy definitions that are ready for you tooassign tooresource groups or subscriptions.</span></span> <span data-ttu-id="10822-109">이러한 기본 제공 정책 및 hello 포털 tooassign 정책을 사용 하 여 때 정의한 사용자 지정 정책은 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10822-109">You see these built-in policies and any custom policies you have defined when using hello portal tooassign policies.</span></span> <span data-ttu-id="10822-110">소개 toopolicies 및 toodefine 사용자 정책을 지정 하는 방법에 대 한 참조 [리소스 정책 개요](resource-manager-policy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="10822-110">For an introduction toopolicies and how toodefine customized policy, see [Resource policy overview](resource-manager-policy.md).</span></span>

<span data-ttu-id="10822-111">정책은 모든 자식 리소스에 의해 상속됩니다.</span><span class="sxs-lookup"><span data-stu-id="10822-111">Policies are inherited by all child resources.</span></span> <span data-ttu-id="10822-112">따라서 정책이 적용 된 tooa 리소스 그룹와 된 경우 해당 리소스 그룹에서 적용 가능한 tooall hello 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="10822-112">So, if a policy is applied tooa resource group, it is applicable tooall hello resources in that resource group.</span></span> <span data-ttu-id="10822-113">이 문서에서는 hello 용어 **범위** toohello 리소스 그룹이 나 hello 정책 할당 된 구독을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="10822-113">In this article, hello term **scope** refers toohello resource group or subscription that is assigned hello policy.</span></span> 

<span data-ttu-id="10822-114">리소스(PUT 및 PATCH 작업)를 만들고 업데이트할 때 정책이 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="10822-114">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

## <a name="assign-a-policy"></a><span data-ttu-id="10822-115">정책 할당</span><span class="sxs-lookup"><span data-stu-id="10822-115">Assign a policy</span></span>

1. <span data-ttu-id="10822-116">tooassign 정책 tooeither 리소스 그룹이 나 구독을 해당 리소스 그룹 또는 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="10822-116">tooassign a policy tooeither a resource group or subscription, select that resource group or subscription.</span></span> <span data-ttu-id="10822-117">Hello 설정에서 선택 **정책**합니다.</span><span class="sxs-lookup"><span data-stu-id="10822-117">In hello settings, select **Policies**.</span></span>

   ![정책 선택](./media/resource-manager-policy-portal/select-policies.png)

2. <span data-ttu-id="10822-119">이 범위에 대 한 정책 할당 toocreate 선택 **할당 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="10822-119">toocreate a policy assignment for this scope, select **Add assignment**.</span></span>

   ![할당 추가](./media/resource-manager-policy-portal/add-assignment.png)

3. <span data-ttu-id="10822-121">Tooassign hello 정책을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="10822-121">Select hello policy you want tooassign.</span></span> <span data-ttu-id="10822-122">모든 정책 정의 tooyour 구독을 추가 하지 않은 경우에 할당에 사용할 수 있는 hello 기본 제공 정책을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="10822-122">Even if you have not added any policy definitions tooyour subscription, you see hello built-in policies that are available for assignment.</span></span> <span data-ttu-id="10822-123">이러한 기본 제공 정책은 여러 일반적인 시나리오에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10822-123">These built-in policies cover many common scenarios.</span></span>

   ![정의 선택](./media/resource-manager-policy-portal/select-definition.png)

4. <span data-ttu-id="10822-125">정책을 선택한 후 hello 정책에 대 한 설명 및 해당 정책에 대 한 매개 변수를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="10822-125">After selecting a policy, you see a description of hello policy, and any parameters for that policy.</span></span> <span data-ttu-id="10822-126">예를 들어 hello 다음 이미지에서는 hello **위치 허용** hello 사용 가능한 위치를 제한 하는 hello 정책에 필요한 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="10822-126">For example, hello following image shows hello **Allowed locations** parameter, which is required for hello policy that restricts hello available locations.</span></span>

   ![매개 변수 표시](./media/resource-manager-policy-portal/show-parameters.png)

5. <span data-ttu-id="10822-128">Hello 사용자 인터페이스를 통해 hello 정책 매개 변수 (예: 배포에 사용할 수 있는 hello 위치)에 대 한 값 toospecify hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="10822-128">Through hello user interface, select hello values toospecify for hello policy parameters (such as hello locations that can be used for deployment).</span></span>

   ![매개 변수 값 선택](./media/resource-manager-policy-portal/select-parameters.png)

6. <span data-ttu-id="10822-130">다른 매개 변수 hello에 대 한 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="10822-130">Provide values for hello other parameters.</span></span> <span data-ttu-id="10822-131">hello 범위 hello 블레이드 hello 정책 할당을 시작할 때 선택에 따라 자동으로 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10822-131">hello scope is automatically assigned based on hello blade you selected when starting hello policy assignment.</span></span> <span data-ttu-id="10822-132">완료되면 **확인** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="10822-132">Select **OK** when done.</span></span>

   ![매개 변수 정의](./media/resource-manager-policy-portal/define-parameters.png)

  <span data-ttu-id="10822-134">Hello 정책 할당 toohello 범위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="10822-134">You have assigned hello policy toohello specified scope.</span></span>

## <a name="view-policy-assignments"></a><span data-ttu-id="10822-135">정책 할당 보기</span><span class="sxs-lookup"><span data-stu-id="10822-135">View policy assignments</span></span>

<span data-ttu-id="10822-136">정책을 할당 한 후에 표시 해당 범위에 대 한 정책 hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="10822-136">After assigning a policy, you see it in hello list of policies for that scope.</span></span> <span data-ttu-id="10822-137">hello **세부 정보** 탭 hello 정책 할당의 요약 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="10822-137">hello **Details** tab shows a summary of hello policy assignment.</span></span>

![세부 정보 표시](./media/resource-manager-policy-portal/show-details.png)

<span data-ttu-id="10822-139">hello **할당 규칙** 탭 hello 정책 정의 대 한 JSON hello를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="10822-139">hello **Assignment rule** tab shows hello JSON for hello policy definition.</span></span>

![할당 규칙 표시](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a><span data-ttu-id="10822-141">기존 정책 할당 변경</span><span class="sxs-lookup"><span data-stu-id="10822-141">Change an existing policy assignment</span></span>

<span data-ttu-id="10822-142">클라이언트는 정책을 toochange 선택 **할당을 편집** 또는 **삭제**</span><span class="sxs-lookup"><span data-stu-id="10822-142">toochange a policy, select **Edit assignment** or **Delete**</span></span>

![할당 편집 또는 삭제](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a><span data-ttu-id="10822-144">사용자 지정 정책 할당</span><span class="sxs-lookup"><span data-stu-id="10822-144">Assign custom policies</span></span>

<span data-ttu-id="10822-145">구독에 사용자 지정 정책을 정의한 경우 해당 정책을 hello 포털을 통해 할당 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10822-145">If you have defined custom policies in your subscription, those policies are available for assignment through hello portal.</span></span> <span data-ttu-id="10822-146">이러한 정책은 앞에 **[Custom]**이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="10822-146">Those policies are prefaced with **[Custom]**</span></span>

![사용자 지정 정책](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a><span data-ttu-id="10822-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="10822-148">Next steps</span></span>
* <span data-ttu-id="10822-149">toolearn 정책을 정의 하기 위한 hello JSON 구문에 대 한 참조 [리소스 정책 개요](resource-manager-policy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="10822-149">toolearn about hello JSON syntax for defining policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="10822-150">기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="10822-150">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="10822-151">에 hello 정책 스키마를 게시 [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="10822-151">hello policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

