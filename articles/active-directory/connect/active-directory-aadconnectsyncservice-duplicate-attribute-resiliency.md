---
title: "ID 동기화 및 중복 특성 복원력 | Microsoft Docs"
description: "Azure AD Connect를 사용하여 디렉터리 동기화 동안 UPN 또는 ProxyAddress 충돌을 사용하여 개체를 처리하는 방법의 새 동작입니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 537a92b7-7a84-4c89-88b0-9bce0eacd931
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.openlocfilehash: 7a8700e70f64851a0c5e5e8c6b31ec7a6884a96c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="identity-synchronization-and-duplicate-attribute-resiliency"></a><span data-ttu-id="1da97-103">ID 동기화 및 중복 특성 복원력</span><span class="sxs-lookup"><span data-stu-id="1da97-103">Identity synchronization and duplicate attribute resiliency</span></span>
<span data-ttu-id="1da97-104">중복 특성 복원력은 Microsoft의 동기화 도구 중 하나를 실행하는 경우 **UserPrincipalName** 및 **ProxyAddress**의 충돌로 발생하는 마찰을 제거하는 Azure Active Directory의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-104">Duplicate Attribute Resiliency is a feature in Azure Active Directory that will eliminate friction caused by **UserPrincipalName** and **ProxyAddress** conflicts when running one of Microsoft’s synchronization tools.</span></span>

<span data-ttu-id="1da97-105">이 두 특성은 일반적으로 지정된 Azure Active Directory 테넌트의 모든 **사용자**, **그룹** 또는 **연락처** 개체에 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-105">These two attributes are generally required to be unique across all **User**, **Group**, or **Contact** objects in a given Azure Active Directory tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="1da97-106">사용자만 UPN을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-106">Only Users can have UPNs.</span></span>
> 
> 

<span data-ttu-id="1da97-107">이 기능이 활성화하는 새 동작은 동기화 파이프라인의 클라우드 부분에 있으므로 클라이언트와 관계 없으며 Azure AD Connect, DirSync 및 MIM + 커넥터를 포함하는 모든 Microsoft 동기화 제품과 관련되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-107">The new behavior that this feature enables is in the cloud portion of the sync pipeline, therefore it is client agnostic and relevant for any Microsoft synchronization product including Azure AD Connect, DirSync and MIM + Connector.</span></span> <span data-ttu-id="1da97-108">일반 용어인 "동기화 클라이언트"는 이 문서에서 이러한 제품 중 하나를 나타내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-108">The generic term “sync client” is used in this document to represent any one of these products.</span></span>

## <a name="current-behavior"></a><span data-ttu-id="1da97-109">현재 동작</span><span class="sxs-lookup"><span data-stu-id="1da97-109">Current behavior</span></span>
<span data-ttu-id="1da97-110">이 고유성 제약 조건을 위반하는 UPN 또는 ProxyAddress 값으로 새 개체를 프로비전하려고 하는 경우 Azure Active Directory는 개체가 생성되는 것을 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-110">If there is an attempt to provision a new object with a UPN or ProxyAddress value that violates this uniqueness constraint, Azure Active Directory blocks that object from being created.</span></span> <span data-ttu-id="1da97-111">마찬가지로 개체가 고유하지 않은 UPN 또는 ProxyAddress로 업데이트되면 업데이트가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-111">Similarly, if an object is updated with a non-unique UPN or ProxyAddress, the update fails.</span></span> <span data-ttu-id="1da97-112">프로비전 시도 또는 업데이트는 각 내보내기 주기 시 동기화 클라이언트에서 다시 시도되고 충돌이 해결될 때까지 계속해서 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-112">The provisioning attempt or update is retried by the sync client upon each export cycle, and continues to fail until the conflict is resolved.</span></span> <span data-ttu-id="1da97-113">각 시도 시 오류 보고서가 발생되고 동기화 클라이언트에서 오류가 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-113">An error report email is generated upon each attempt and an error is logged by the sync client.</span></span>

## <a name="behavior-with-duplicate-attribute-resiliency"></a><span data-ttu-id="1da97-114">중복 특성 복원력으로 동작</span><span class="sxs-lookup"><span data-stu-id="1da97-114">Behavior with Duplicate Attribute Resiliency</span></span>
<span data-ttu-id="1da97-115">중복 특성으로 개체 프로비전 또는 업데이트에 완전히 실패하는 대신 Azure Active Directory는 고유성 제약 조건을 위반하는 중복 특성을 “격리합니다”.</span><span class="sxs-lookup"><span data-stu-id="1da97-115">Instead of completely failing to provision or update an object with a duplicate attribute, Azure Active Directory “quarantines” the duplicate attribute which would violate the uniqueness constraint.</span></span> <span data-ttu-id="1da97-116">이 특성이 UserPrincipalName과 같은 프로비전에 필요한 경우 서비스는 자리 표시자 값을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-116">If this attribute is required for provisioning, like UserPrincipalName, the service assigns a placeholder value.</span></span> <span data-ttu-id="1da97-117">이러한 임시 값의 형식은</span><span class="sxs-lookup"><span data-stu-id="1da97-117">The format of these temporary values is</span></span>  
<span data-ttu-id="1da97-118">“***<OriginalPrefix>+<4DigitNumber>@<InitialTenantDomain>.onmicrosoft.com***”.</span><span class="sxs-lookup"><span data-stu-id="1da97-118">“***<OriginalPrefix>+<4DigitNumber>@<InitialTenantDomain>.onmicrosoft.com***”.</span></span>  
<span data-ttu-id="1da97-119">**ProxyAddress**와 같은 특성이 필요하지 않은 경우 Azure Active Directory는 단순히 충돌 특성을 격리하고 개체 생성 또는 업데이트를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-119">If the attribute is not required, like a  **ProxyAddress**, Azure Active Directory simply quarantines the conflict attribute and proceeds with the object creation or update.</span></span>

<span data-ttu-id="1da97-120">특성을 격리 시 충돌에 대한 정보는 이전 동작에 사용된 동일한 오류 보고서 전자 메일에 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-120">Upon quarantining the attribute, information about the conflict is sent in the same error report email used in the old behavior.</span></span> <span data-ttu-id="1da97-121">그러나 격리가 발생할 때 이 정보는 오류 보고서에 한 번만 표시되며 이후 메일에 계속해서 기록되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-121">However, this info only appears in the error report one time, when the quarantine happens, it does not continue to be logged in future emails.</span></span> <span data-ttu-id="1da97-122">또한 이 개체에 대한 내보내기가 성공했으므로 동기화 클라이언트는 오류를 기록하지 않고 후속 동기화 주기 시 만들기 / 업데이트 작업을 시도하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-122">Also, since the export for this object has succeeded, the sync client does not log an error and does not retry the create / update operation upon subsequent sync cycles.</span></span>

<span data-ttu-id="1da97-123">이 동작을 지원하기 위해 사용자, 그룹 및 연락처 개체 클래스: </span><span class="sxs-lookup"><span data-stu-id="1da97-123">To support this behavior a new attribute has been added to the User, Group, and Contact object classes:</span></span>  
<span data-ttu-id="1da97-124">**DirSyncProvisioningError**</span><span class="sxs-lookup"><span data-stu-id="1da97-124">**DirSyncProvisioningErrors**</span></span>

<span data-ttu-id="1da97-125">정상적으로 추가해야 하는 고유성 제약 조건을 위반하는 충돌 특성을 저장하는 데 사용되는 다중값 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-125">This is a multi-valued attribute that is used to store the conflicting attributes that would violate the uniqueness constraint should they be added normally.</span></span> <span data-ttu-id="1da97-126">해결된 중복 특성 충돌을 찾기 위해 1시간마다 실행되고 격리에서 문제의 특성을 자동으로 제거하는 백그라운드 타이머 작업이 Azure Active Directory에서 활성화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-126">A background timer task has been enabled in Azure Active Directory that  runs every hour to look for duplicate attribute conflicts that have been resolved, and automatically removes the attributes in question from quarantine.</span></span>

### <a name="enabling-duplicate-attribute-resiliency"></a><span data-ttu-id="1da97-127">중복 특성 복원력 활성화</span><span class="sxs-lookup"><span data-stu-id="1da97-127">Enabling Duplicate Attribute Resiliency</span></span>
<span data-ttu-id="1da97-128">중복 특성 복원력은 모든 Azure Active Directory 테넌트의 새로운 기본 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-128">Duplicate Attribute Resiliency will be the new default behavior across all Azure Active Directory tenants.</span></span> <span data-ttu-id="1da97-129">2016년 8월 22일 또는 그 이후에 동기화를 처음으로 사용하는 모든 테넌트에 기본적으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-129">It will be on by default for all tenants that enabled synchronization for the first time on August 22nd, 2016 or later.</span></span> <span data-ttu-id="1da97-130">이 날짜 이전에 동기화를 사용하도록 설정한 테넌트에는 이 기능이 일괄적으로 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-130">Tenants that enabled sync prior to this date will have the feature enabled in batches.</span></span> <span data-ttu-id="1da97-131">이 출시는 2016년 9월에 시작되며 기능이 사용되는 특정 날짜와 함께 각 테넌트의 기술 알림 담당자에게 전자 메일 알림이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-131">This rollout will begin in September 2016, and an email notification will be sent to each tenant's technical notification contact with the specific date when the feature will be enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="1da97-132">중복 특성 복원력이 설정된 후에는 해제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-132">Once Duplicate Attribute Resiliency has been turned on it cannot be disabled.</span></span>

<span data-ttu-id="1da97-133">이 기능이 테넌트에 사용되는지 확인하려면 Azure Active Directory PowerShell 모듈의 최신 버전을 다운로드하여 다음을 실행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-133">To check if the feature is enabled for your tenant, you can do so by downloading the latest version of the Azure Active Directory PowerShell module and running:</span></span>

`Get-MsolDirSyncFeatures -Feature DuplicateUPNResiliency`

`Get-MsolDirSyncFeatures -Feature DuplicateProxyAddressResiliency`

> [!NOTE]
> <span data-ttu-id="1da97-134">이제는 중복 특성 복원력 기능을 사용자 테넌트에서 켜기 전에 사전에 활성화하는 데 Set-MsolDirSyncFeature cmdlet을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-134">You can no longer use Set-MsolDirSyncFeature cmdlet to proactively enable the Duplicate Attribute Resiliency feature before it is turned on for your tenant.</span></span> <span data-ttu-id="1da97-135">기능을 테스트하려면 새로운 Azure Active Directory 테넌트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-135">To be able to test the feature, you will need to create a new Azure Active Directory tenant.</span></span>

## <a name="identifying-objects-with-dirsyncprovisioningerrors"></a><span data-ttu-id="1da97-136">DirSyncProvisioningErrors로 개체 식별</span><span class="sxs-lookup"><span data-stu-id="1da97-136">Identifying Objects with DirSyncProvisioningErrors</span></span>
<span data-ttu-id="1da97-137">중복 속성 충돌로 인해 이러한 오류가 있는 개체를 식별하는 방법은 현재 PowerShell Azure Active Directory 및 Office 365 관리자 포털로 두 가지 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-137">There are currently two methods to identify objects that have these errors due to duplicate property conflicts, Azure Active Directory PowerShell and the Office 365 Admin Portal.</span></span> <span data-ttu-id="1da97-138">향후 보고에 기반한 추가 포털로 확장할 계획이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-138">There are plans to extend to additional portal based reporting in the future.</span></span>

### <a name="azure-active-directory-powershell"></a><span data-ttu-id="1da97-139">Azure Active Directory PowerShell</span><span class="sxs-lookup"><span data-stu-id="1da97-139">Azure Active Directory PowerShell</span></span>
<span data-ttu-id="1da97-140">이 항목에서 PowerShell cmdlet의 경우 다음은 true입니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-140">For the PowerShell cmdlets in this topic, the following is true:</span></span>

* <span data-ttu-id="1da97-141">다음 cmdlet은 모두 대/소문자 구분입니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-141">All of the following cmdlets are case sensitive.</span></span>
* <span data-ttu-id="1da97-142">**–ErrorCategory PropertyConflict**는 항상 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-142">The **–ErrorCategory PropertyConflict** must always be included.</span></span> <span data-ttu-id="1da97-143">현재 다른 종류의 **ErrorCategory**는 없지만 나중에 확장될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-143">There are currently no other types of **ErrorCategory**, but this may be extended in the future.</span></span>

<span data-ttu-id="1da97-144">먼저 **Connect-MsolService**를 실행하고 테넌트 관리자에 대한 자격 증명을 입력하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-144">First, get started by running **Connect-MsolService** and entering credentials for a tenant administrator.</span></span>

<span data-ttu-id="1da97-145">그런 다음 다양한 방법으로 오류를 보려면 다음 cmdlet 및 연산자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-145">Then, use the following cmdlets and operators to view errors in different ways:</span></span>

1. [<span data-ttu-id="1da97-146">모두 표시</span><span class="sxs-lookup"><span data-stu-id="1da97-146">See All</span></span>](#see-all)
2. [<span data-ttu-id="1da97-147">속성 형식으로</span><span class="sxs-lookup"><span data-stu-id="1da97-147">By Property Type</span></span>](#by-property-type)
3. [<span data-ttu-id="1da97-148">충돌 값으로</span><span class="sxs-lookup"><span data-stu-id="1da97-148">By Conflicting Value</span></span>](#by-conflicting-value)
4. [<span data-ttu-id="1da97-149">문자열 검색을 사용하여</span><span class="sxs-lookup"><span data-stu-id="1da97-149">Using a String Search</span></span>](#using-a-string-search)
5. [<span data-ttu-id="1da97-150">정렬</span><span class="sxs-lookup"><span data-stu-id="1da97-150">Sorted</span></span>](#sorted)
6. [<span data-ttu-id="1da97-151">제한된 수량 또는 모두</span><span class="sxs-lookup"><span data-stu-id="1da97-151">In a Limited Quantity or All</span></span>](#in-a-limited-quantity-or-all)

#### <a name="see-all"></a><span data-ttu-id="1da97-152">모두 표시</span><span class="sxs-lookup"><span data-stu-id="1da97-152">See all</span></span>
<span data-ttu-id="1da97-153">연결되면 테넌트에서 오류를 프로비저닝하는 특성의 일반 목록을 보기 위해 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-153">Once connected, to see a general list of attribute provisioning errors in the tenant run:</span></span>

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict`

<span data-ttu-id="1da97-154">다음과 같은 결과가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-154">This produces a result like the following:</span></span>  
 <span data-ttu-id="1da97-155">![Get MsolDirSyncProvisioningError](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1.png "Get MsolDirSyncProvisioningError")</span><span class="sxs-lookup"><span data-stu-id="1da97-155">![Get-MsolDirSyncProvisioningError](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1.png "Get-MsolDirSyncProvisioningError")</span></span>  

#### <a name="by-property-type"></a><span data-ttu-id="1da97-156">속성 형식으로</span><span class="sxs-lookup"><span data-stu-id="1da97-156">By property type</span></span>
<span data-ttu-id="1da97-157">속성 형식으로 오류를 보려면 **UserPrincipalName** 또는 **ProxyAddresses** 인수를 가진 **-PropertyName** 플래그를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-157">To see errors by property type, add the **-PropertyName** flag with the **UserPrincipalName** or **ProxyAddresses** argument:</span></span>

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName UserPrincipalName`

<span data-ttu-id="1da97-158">또는</span><span class="sxs-lookup"><span data-stu-id="1da97-158">Or</span></span>

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName ProxyAddresses`

#### <a name="by-conflicting-value"></a><span data-ttu-id="1da97-159">충돌 값으로</span><span class="sxs-lookup"><span data-stu-id="1da97-159">By conflicting value</span></span>
<span data-ttu-id="1da97-160">특정 속성에 관련된 오류를 확인하려면 **-PropertyValue** 플래그를 추가합니다(이 플래그를 추가하는 경우 **-PropertyName**을 함께 사용해야 함).</span><span class="sxs-lookup"><span data-stu-id="1da97-160">To see errors relating to a specific property add the **-PropertyValue** flag (**-PropertyName** must be used as well when adding this flag):</span></span>

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyValue User@domain.com -PropertyName UserPrincipalName`

#### <a name="using-a-string-search"></a><span data-ttu-id="1da97-161">문자열 검색을 사용하여</span><span class="sxs-lookup"><span data-stu-id="1da97-161">Using a string search</span></span>
<span data-ttu-id="1da97-162">광범위한 문자열 검색을 수행하려면 **-SearchString** 플래그를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-162">To do a broad string search use the **-SearchString** flag.</span></span> <span data-ttu-id="1da97-163">항상 필수 항목인 **-ErrorCategory PropertyConflict**를 제외하고 위의 모든 플래그와 독립적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-163">This can be used independently from all of the above flags, with the exception of **-ErrorCategory PropertyConflict**, which is always required:</span></span>

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -SearchString User`

#### <a name="in-a-limited-quantity-or-all"></a><span data-ttu-id="1da97-164">제한된 수량 또는 모두</span><span class="sxs-lookup"><span data-stu-id="1da97-164">In a limited quantity or all</span></span>
1. <span data-ttu-id="1da97-165">**MaxResults<Int>**는 특정 값으로 쿼리를 제한하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-165">**MaxResults <Int>** can be used to limit the query to a specific number of values.</span></span>
2. <span data-ttu-id="1da97-166">**All** 은 많은 오류가 있는 경우 검색되는 모든 결과를 확인하기 위해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-166">**All** can be used to ensure all results are retrieved in the case that a large number of errors exists.</span></span>

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -MaxResults 5`

## <a name="office-365-admin-portal"></a><span data-ttu-id="1da97-167">Office 365 관리 포털</span><span class="sxs-lookup"><span data-stu-id="1da97-167">Office 365 admin portal</span></span>
<span data-ttu-id="1da97-168">Office 365 관리 센터에서 디렉터리 동기화 오류를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-168">You can view directory synchronization errors in the Office 365 admin center.</span></span> <span data-ttu-id="1da97-169">Office 365 포털의 보고서는 이러한 오류가 있는 **사용자** 개체만을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-169">The report in the Office 365 portal only displays **User** objects that have these errors.</span></span> <span data-ttu-id="1da97-170">**그룹** 및 **연락처** 간의 충돌에 대한 정보는 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-170">It does not show info about conflicts between **Groups** and **Contacts**.</span></span>

<span data-ttu-id="1da97-171">![활성 사용자](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1234.png "활성 사용자")</span><span class="sxs-lookup"><span data-stu-id="1da97-171">![Active Users](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1234.png "Active Users")</span></span>

<span data-ttu-id="1da97-172">Office 365 관리 센터에서 디렉터리 동기화 오류를 보는 방법에 대한 지침은 [Office 365에서 디렉터리 동기화 오류 확인](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1da97-172">For instructions on how to view directory synchronization errors in the Office 365 admin center, see [Identify directory synchronization errors in Office 365](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067).</span></span>

### <a name="identity-synchronization-error-report"></a><span data-ttu-id="1da97-173">ID 동기화 오류 보고서</span><span class="sxs-lookup"><span data-stu-id="1da97-173">Identity synchronization error report</span></span>
<span data-ttu-id="1da97-174">중복 특성 충돌이 있는 개체가 이 새 동작으로 처리되는 경우 알림은 테넌트에 대한 기술 알림 문의로 전송되는 표준 ID 동기화 오류 보고서 전자 메일에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-174">When an object with a duplicate attribute conflict is handled with this new behavior a notification is included in the standard Identity Synchronization Error Report email that is sent to the Technical Notification contact for the tenant.</span></span> <span data-ttu-id="1da97-175">그러나 이 동작에서 중요한 변경 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-175">However, there is an important change in this behavior.</span></span> <span data-ttu-id="1da97-176">이전에 중복 특성 충돌에 대한 정보는 충돌이 해결될 때까지 모든 후속 오류 보고서에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-176">In the past, information about a duplicate attribute conflict would be included in every subsequent error report until the conflict was resolved.</span></span> <span data-ttu-id="1da97-177">이 새 동작으로 지정된 충돌에 대한 오류 알림이 충돌 특성이 격리되는 시간에 한 번만 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-177">With this new behavior, the error notification for a given conflict does only appear once- at the time the conflicting attribute is quarantined.</span></span>

<span data-ttu-id="1da97-178">ProxyAddress 충돌에 대한 메일 알림의 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-178">Here is an example of what the email notification looks like for a ProxyAddress conflict:</span></span>  
    <span data-ttu-id="1da97-179">![활성 사용자](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "활성 사용자")</span><span class="sxs-lookup"><span data-stu-id="1da97-179">![Active Users](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "Active Users")</span></span>  

## <a name="resolving-conflicts"></a><span data-ttu-id="1da97-180">충돌 해결</span><span class="sxs-lookup"><span data-stu-id="1da97-180">Resolving conflicts</span></span>
<span data-ttu-id="1da97-181">이러한 오류에 대한 문제 해결 전략 및 해결 방법은 중복 특성 오류가 이전에 처리된 방식과 다르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-181">Troubleshooting strategy and resolution tactics for these errors should not differ from the way duplicate attribute errors were handled in the past.</span></span> <span data-ttu-id="1da97-182">유일한 차이점은 타이머 작업은 서비스쪽 테넌트를 통해 스윕하여 충돌이 해결되면 적절한 개체에 문제의 특성을 자동으로 추가한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-182">The only difference is that the timer task sweeps through the tenant on the service-side to automatically add the attribute in question to the proper object once the conflict is resolved.</span></span>

<span data-ttu-id="1da97-183">다음 문서에서는 다양한 문제 해결 및 해결 방법을 간략하게 설명합니다. [Office 365에서 중복되거나 잘못된 특성이 디렉터리 동기화를 방해할 경우](https://support.microsoft.com/kb/2647098).</span><span class="sxs-lookup"><span data-stu-id="1da97-183">The following article outlines various troubleshooting and resolution strategies: [Duplicate or invalid attributes prevent directory synchronization in Office 365](https://support.microsoft.com/kb/2647098).</span></span>

## <a name="known-issues"></a><span data-ttu-id="1da97-184">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="1da97-184">Known issues</span></span>
<span data-ttu-id="1da97-185">이러한 알려진 문제로 인해 데이터 손실 또는 서비스 저하가 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-185">None of these known issues causes data loss or service degradation.</span></span> <span data-ttu-id="1da97-186">그 중 일부는 심미적이며 다른 것은 충돌 특성을 격리하는 대신 표준 “*사전 복원력*” 중복 특성 오류를 throw하고 다른 것은 추가 수동 수정이 필요한 특정 오류를 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-186">Several of them are aesthetic, others cause standard “*pre-resiliency*” duplicate attribute errors to be thrown instead of quarantining the conflict attribute, and another causes certain errors to require extra manual fix-up.</span></span>

<span data-ttu-id="1da97-187">**핵심 동작:**</span><span class="sxs-lookup"><span data-stu-id="1da97-187">**Core behavior:**</span></span>

1. <span data-ttu-id="1da97-188">특정 특성 구성이 있는 개체는 격리되는 중복 특성과 달리 내보내기 오류가 계속 수신됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-188">Objects with specific attribute configurations continue to receive export errors as opposed to the duplicate attribute(s) being quarantined.</span></span>  
   <span data-ttu-id="1da97-189">예:</span><span class="sxs-lookup"><span data-stu-id="1da97-189">For example:</span></span>
   
    <span data-ttu-id="1da97-190">a.</span><span class="sxs-lookup"><span data-stu-id="1da97-190">a.</span></span> <span data-ttu-id="1da97-191">새로운 사용자가 **Joe@contoso.com**의 UPN과 ProxyAddress **smtp:Joe@contoso.com**로 AD에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-191">New user is created in AD with a UPN of **Joe@contoso.com** and ProxyAddress **smtp:Joe@contoso.com**</span></span>
   
    <span data-ttu-id="1da97-192">b.</span><span class="sxs-lookup"><span data-stu-id="1da97-192">b.</span></span> <span data-ttu-id="1da97-193">이 개체의 속성이 ProxyAddress가 **SMTP:Joe@contoso.com**인 기존 그룹과 충돌합니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-193">The properties of this object conflict with an existing Group, where ProxyAddress is **SMTP:Joe@contoso.com**.</span></span>
   
    <span data-ttu-id="1da97-194">c.</span><span class="sxs-lookup"><span data-stu-id="1da97-194">c.</span></span> <span data-ttu-id="1da97-195">내보낼 때 충돌 특성이 격리되는 대신 **ProxyAddress 충돌** 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-195">Upon export, a **ProxyAddress conflict** error is thrown instead of having the conflict attributes quarantined.</span></span> <span data-ttu-id="1da97-196">복구 기능이 활성화되기 전에 수행되므로 각 후속 동기화 주기 시 작업이 다시 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-196">The operation is retried upon each subsequent sync cycle, as it would have been before the resiliency feature was enabled.</span></span>
2. <span data-ttu-id="1da97-197">두 그룹이 동일한 SMTP 주소로 온-프레미스가 생성되는 경우 하나는 첫 번째 시도에서 표준 중복 **ProxyAddress** 오류로 프로비전하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-197">If two Groups are created on-premises with the same SMTP address, one fails to provision on the first attempt with a standard duplicate **ProxyAddress** error.</span></span> <span data-ttu-id="1da97-198">그러나 다음 동기화 주기 시 중복 값은 제대로 격리됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-198">However, the duplicate value is properly quarantined upon the next sync cycle.</span></span>

<span data-ttu-id="1da97-199">**Office 포털 보고서**:</span><span class="sxs-lookup"><span data-stu-id="1da97-199">**Office Portal Report**:</span></span>

1. <span data-ttu-id="1da97-200">UPN 충돌 집합에서 두 개체에 대한 자세한 오류 메시지는 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-200">The detailed error message for two objects in a UPN conflict set is the same.</span></span> <span data-ttu-id="1da97-201">이는 실제로 하나에만 변경된 데이터가 있는 경우 둘 모두 해당 UPN을 변경 / 격리했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-201">This indicates that they have both had their UPN changed / quarantined, when in fact only a one of them had any data changed.</span></span>
2. <span data-ttu-id="1da97-202">UPN 충돌에 대한 자세한 오류 메시지는 해당 UPN을 변경하고 격리한 사용자에 대한 잘못된 displayName을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-202">The detailed error message for a UPN conflict shows the wrong displayName for a user who has had their UPN changed/quarantined.</span></span> <span data-ttu-id="1da97-203">예:</span><span class="sxs-lookup"><span data-stu-id="1da97-203">For example:</span></span>
   
    <span data-ttu-id="1da97-204">a.</span><span class="sxs-lookup"><span data-stu-id="1da97-204">a.</span></span> <span data-ttu-id="1da97-205">**사용자 A**는 먼저 **UPN = User@contoso.com**과 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-205">**User A** syncs up first with **UPN = User@contoso.com**.</span></span>
   
    <span data-ttu-id="1da97-206">b.</span><span class="sxs-lookup"><span data-stu-id="1da97-206">b.</span></span> <span data-ttu-id="1da97-207">**사용자 B**는 **UPN = User@contoso.com**과 동기화하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-207">**User B** is attempted to be synced up next with **UPN = User@contoso.com**.</span></span>
   
    <span data-ttu-id="1da97-208">c.</span><span class="sxs-lookup"><span data-stu-id="1da97-208">c.</span></span> <span data-ttu-id="1da97-209">**사용자 B**의 UPN은 **User1234@contoso.onmicrosoft.com**로 변경되며 **User@contoso.com**이 **DirSyncProvisioningErrors**에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-209">**User B’s** UPN is changed to **User1234@contoso.onmicrosoft.com** and **User@contoso.com** is added to **DirSyncProvisioningErrors**.</span></span>
   
    <span data-ttu-id="1da97-210">d.</span><span class="sxs-lookup"><span data-stu-id="1da97-210">d.</span></span> <span data-ttu-id="1da97-211">**사용자 B**에 대한 오류 메시지는 **사용자 A**가 이미 **User@contoso.com**을 UPN으로 가지고 있음을 나타내야 하지만 **사용자 B** 고유의 displayName을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-211">The error message for **User B** should indicate that **User A** already has **User@contoso.com** as a UPN, but it shows **User B’s** own displayName.</span></span>

<span data-ttu-id="1da97-212">**ID 동기화 오류 보고서**:</span><span class="sxs-lookup"><span data-stu-id="1da97-212">**Identity synchronization error report**:</span></span>

<span data-ttu-id="1da97-213">*이 문제를 해결하는 방법에 대한 단계*의 링크가 잘못되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-213">The link for *steps on how to resolve this issue* is incorrect:</span></span>  
    <span data-ttu-id="1da97-214">![활성 사용자](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "활성 사용자")</span><span class="sxs-lookup"><span data-stu-id="1da97-214">![Active Users](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "Active Users")</span></span>  

<span data-ttu-id="1da97-215">[https://aka.ms/duplicateattributeresiliency](https://aka.ms/duplicateattributeresiliency)를 가리켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1da97-215">It should point to [https://aka.ms/duplicateattributeresiliency](https://aka.ms/duplicateattributeresiliency).</span></span>

## <a name="see-also"></a><span data-ttu-id="1da97-216">참고 항목</span><span class="sxs-lookup"><span data-stu-id="1da97-216">See also</span></span>
* [<span data-ttu-id="1da97-217">Azure AD Connect 동기화</span><span class="sxs-lookup"><span data-stu-id="1da97-217">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="1da97-218">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="1da97-218">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
* [<span data-ttu-id="1da97-219">Office 365에서 디렉터리 동기화 오류 확인</span><span class="sxs-lookup"><span data-stu-id="1da97-219">Identify directory synchronization errors in Office 365</span></span>](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067)

