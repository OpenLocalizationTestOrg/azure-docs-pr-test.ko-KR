---
title: "Azure AD 특성 매핑 사용자 지정 | Microsoft Docs"
description: "Azure Active Directory의 Saas 앱에 대한 어떤 특성 매핑이 있고 어떻게 비즈니스 요구 사항에 맞게 수정하는지를 알아봅니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 549e0b8c-87ce-4c9b-b487-b7bf0155dc77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6ca2fdc9c68ea0030d938eeaebd57aafa0e2790f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a><span data-ttu-id="dc7b2-103">Azure Active Directory에서 SaaS 응용 프로그램에 대한 사용자 프로비전 특성 매핑 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="dc7b2-103">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>
<span data-ttu-id="dc7b2-104">Microsoft Azure AD는 Salesforce, Google Apps 등과 같은 타사 SaaS 응용 프로그램에 프로비전을 하는 사용자에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-104">Microsoft Azure AD provides support for user provisioning to third-party SaaS applications such as Salesforce, Google Apps and others.</span></span> <span data-ttu-id="dc7b2-105">타사 SaaS 응용 프로그램을 프로비전하는 사용자가 있을 경우 Azure 관리 포털은 그 특성 값을 “특성 매핑”이라고 하는 구성 형태로 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-105">If you have user provisioning for a third-party SaaS application enabled, the Azure Management Portal controls its attribute values in form of a configuration called “attribute mapping.”</span></span>

<span data-ttu-id="dc7b2-106">Azure AD 사용자 개체와 각 SaaS 앱의 사용자 개체 사이에는 미리 구성된 특성 세트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-106">There is a preconfigured set of attribute mappings between Azure AD user objects and each SaaS app’s user objects.</span></span> <span data-ttu-id="dc7b2-107">일부 앱은 그룹이나 연락처 같은 다른 유형의 개체를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-107">Some apps manage other types of objects, such as Groups or Contacts.</span></span> <br> 
 <span data-ttu-id="dc7b2-108">비즈니스 요구 사항에 따라 기본 특성 매핑을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-108">You can customize the default attribute mappings according to your business needs.</span></span> <span data-ttu-id="dc7b2-109">즉, 기존의 특성 매핑을 변경 또는 삭제하거나 새 특성 매핑을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-109">This means, you can change or delete existing attribute mappings or create new attribute mappings.</span></span>

<span data-ttu-id="dc7b2-110">Azure AD 포털에서 **엔터프라이즈 응용 프로그램**의 **관리** 섹션에 있는 **프로비전** 아래 **매핑** 구성을 클릭하여 이 기능에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-110">In the Azure AD portal, you can access this feature by clicking a **Mappings** configuration under **Provisioning** in the **Manage** section of an **Enterprise application**.</span></span>


![Salesforce][5] 

<span data-ttu-id="dc7b2-112">**매핑** 구성을 클릭하면 관련 **특성 매핑** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-112">Clicking a **Mappings** configuration, opens the related **Attribute Mapping** blade.</span></span>  
<span data-ttu-id="dc7b2-113">SaaS 응용 프로그램에서 올바르게 작동하기 위해 요구되는 특성 매핑이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-113">There are attribute mappings that are required by a SaaS application to function correctly.</span></span> <span data-ttu-id="dc7b2-114">필수 특성인 경우 **삭제** 기능을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-114">For required attributes, the **Delete** feature is unavailable.</span></span>


![Salesforce][6]  

<span data-ttu-id="dc7b2-116">위의 예제를 통해 Salesforce에서 관리된 개체의 **Username** 특성이 그 연결된 Azure Active Directory 개체의 **userPrincipalName** 값으로 채워지는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-116">In the example above, you can see that the **Username** attribute of a managed object in Salesforce is populated with the **userPrincipalName** value of the linked Azure Active Directory Object.</span></span>

<span data-ttu-id="dc7b2-117">매핑을 클릭하여 기존 **특성 매핑**을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-117">You can customize existing **Attribute Mappings** by clicking a mapping.</span></span> <span data-ttu-id="dc7b2-118">그러면 **특성 편집** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-118">This opens the **Edit Attribute** blade.</span></span>

![Salesforce][7]  


  

## <a name="understanding-attribute-mapping-types"></a><span data-ttu-id="dc7b2-120">특성 매핑 유형 이해</span><span class="sxs-lookup"><span data-stu-id="dc7b2-120">Understanding attribute mapping types</span></span>
<span data-ttu-id="dc7b2-121">특성 매핑으로 타사 SaaS 응용 프로그램에서 특성이 채워지는 법을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-121">With attribute mappings, you control how attributes are populated in a third-party SaaS application.</span></span> <span data-ttu-id="dc7b2-122">4 가지의 다른 매핑 형식이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-122">There are four different mapping types supported:</span></span>

* <span data-ttu-id="dc7b2-123">**직접** – 대상 특성이 Azure AD에서 연결된 개체의 특성 값으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-123">**Direct** – the target attribute is populated with the value of an attribute of the linked object in Azure AD.</span></span>
* <span data-ttu-id="dc7b2-124">**상수** – 대상 특성이 지정된 특정 문자열로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-124">**Constant** – the target attribute is populated with a specific string you have specified.</span></span>
* <span data-ttu-id="dc7b2-125">**식** - 대상 특성이 스크립트 방식의 식의 결과에 따라 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-125">**Expression** - the target attribute is populated based on the result of a script-like expression.</span></span> 
  <span data-ttu-id="dc7b2-126">자세한 내용은 [Azure Active Directory의 특성 매핑에 대한 식 작성](active-directory-saas-writing-expressions-for-attribute-mappings.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-126">For more information, see [Writing Expressions for Attribute Mappings in Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>
* <span data-ttu-id="dc7b2-127">**None** - 대상 특성이 수정되지 않고 남아있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-127">**None** - the target attribute is left unmodified.</span></span> <span data-ttu-id="dc7b2-128">그러나 대상 특성이 비어 있으면 지정된 기본 값으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-128">However, if the target attribute is ever empty, it is populated with the Default value that you specify.</span></span>

<span data-ttu-id="dc7b2-129">이 네 가지 기본 특성 맵 형식 외에도 사용자 지정 특성 매핑은 **기본** 값 할당(선택 사항)의 개념을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-129">In addition to these four basic attribute mapping types, custom attribute mappings support the concept of an optional **default** value assignment.</span></span> <span data-ttu-id="dc7b2-130">기본 값 할당은 Azure AD에나 대상 개체에 값이 없을 경우 대상 특성이 값으로 채워지는지 확인해줍니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-130">The default value assignment ensures that a target attribute is populated with a value if there is neither a value in Azure AD nor on the target object.</span></span> <span data-ttu-id="dc7b2-131">이 값을 비워두는 것이 가장 일반적인 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-131">The most common configuration is to leave this blank.</span></span>


## <a name="understanding-attribute-mapping-properties"></a><span data-ttu-id="dc7b2-132">특성 매핑 속성 이해</span><span class="sxs-lookup"><span data-stu-id="dc7b2-132">Understanding attribute mapping properties</span></span>

<span data-ttu-id="dc7b2-133">이전 섹션에서 특성 매핑 유형 속성에 대해 이미 소개한 바 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-133">In the previous section, you have already been introduced to the attribute mapping type property.</span></span>
<span data-ttu-id="dc7b2-134">이 속성 외에도, 특성 매핑은 다음 특성도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-134">In addition to this property, attribute mappings do also support the following attributes:</span></span>

- <span data-ttu-id="dc7b2-135">**원본 특성** - 원본 시스템의 사용자 특성(예: Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="dc7b2-135">**Source attribute** - The user attribute from the source system (e.g.: Azure Active Directory).</span></span>
- <span data-ttu-id="dc7b2-136">**대상 특성** – 대상 시스템의 사용자 특성(예: ServiceNow).</span><span class="sxs-lookup"><span data-stu-id="dc7b2-136">**Target attribute** – The user attribute in the target system (e.g.: ServiceNow).</span></span>
- <span data-ttu-id="dc7b2-137">**이 특성을 사용하여 개체 일치** – 원본 및 대상 시스템 간에 사용자를 고유하게 식별하는 데 이 매핑을 사용할지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-137">**Match objects using this attribute** – Whether or not this mapping should be used to uniquely identify users between the source and target systems.</span></span> <span data-ttu-id="dc7b2-138">일반적으로 대상 응용 프로그램에서 username 필드에 매핑되는 Azure AD의 userPrincipalName 또는 메일 특성에서 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-138">This is typically set on the userPrincipalName or mail attribute in Azure AD, which is typically mapped to a username field in a target application.</span></span>
- <span data-ttu-id="dc7b2-139">**일치 우선 순위** – 여러 일치 특성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-139">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="dc7b2-140">일치 특성이 여러 개 있으면 이 필드에 정의된 순서대로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-140">When there are multiple, they are evaluated in the order defined by this field.</span></span> <span data-ttu-id="dc7b2-141">일치 항목이 발견되는 즉시 더 이상 일치 특성을 평가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-141">As soon as a match is found, no further matching attributes are evaluated.</span></span>
- <span data-ttu-id="dc7b2-142">**이 매핑 적용**</span><span class="sxs-lookup"><span data-stu-id="dc7b2-142">**Apply this mapping**</span></span>
    - <span data-ttu-id="dc7b2-143">**항상** – 사용자 만들기 및 업데이트 작업 시 이 매핑을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-143">**Always** – Apply this mapping on both user creation and update actions</span></span>
    - <span data-ttu-id="dc7b2-144">**만들기 작업 시에만** - 사용자 만들기 작업 시에만 이 매핑을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-144">**Only during creation** - Apply this mapping only on user creation actions</span></span>


## <a name="what-you-should-know"></a><span data-ttu-id="dc7b2-145">알아야 할 사항</span><span class="sxs-lookup"><span data-stu-id="dc7b2-145">What you should know</span></span>

<span data-ttu-id="dc7b2-146">Microsoft Azure AD는 동기화 프로세스의 효과적인 구현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-146">Microsoft Azure AD provides an efficient implementation of a synchronization process.</span></span> <span data-ttu-id="dc7b2-147">초기화된 환경에서 동기화 주기 중에는 업데이트가 필요한 개체만 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-147">In an initialized environment, only objects requiring updates are processed during a synchronization cycle.</span></span> <span data-ttu-id="dc7b2-148">특성 매핑 업데이트는 동기화 주기의 성능에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-148">Updating attribute mappings has an impact on the performance of a synchronization cycle.</span></span> <span data-ttu-id="dc7b2-149">특성 매핑 구성의 업데이트는 모든 관리된 개체를 다시 평가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-149">An update to the attribute mapping configuration requires all managed objects to be reevaluated.</span></span> <span data-ttu-id="dc7b2-150">특성 매핑에 대한 연속 변경 횟수를 최소로 유지하는 것이 가장 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="dc7b2-150">It is a recommended best practice to keep the number of consecutive changes to your attribute mappings at a minimum.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc7b2-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dc7b2-151">Next steps</span></span>

* [<span data-ttu-id="dc7b2-152">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="dc7b2-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="dc7b2-153">SaaS 앱에 자동화된 사용자 프로비전/프로비전 해제</span><span class="sxs-lookup"><span data-stu-id="dc7b2-153">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="dc7b2-154">특성 매핑에 대한 식 작성</span><span class="sxs-lookup"><span data-stu-id="dc7b2-154">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="dc7b2-155">사용자 프로 비전에 대 한 필터 범위 지정</span><span class="sxs-lookup"><span data-stu-id="dc7b2-155">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="dc7b2-156">SCIM를 사용하여 Azure Active Directory으로부터 응용 프로그램에 사용자 및 그룹의 자동 프로비전 사용</span><span class="sxs-lookup"><span data-stu-id="dc7b2-156">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="dc7b2-157">계정 프로비전 알림</span><span class="sxs-lookup"><span data-stu-id="dc7b2-157">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="dc7b2-158">SaaS App을 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="dc7b2-158">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png

