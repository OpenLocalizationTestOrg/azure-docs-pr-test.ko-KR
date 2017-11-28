---
title: "aaaIdentity 동기화 및 중복 특성 복원 력 | Microsoft Docs"
description: "어떻게 toohandle 개체와 함께 UPN 또는 / / ProxyAddress 충돌 하는 동안 Azure AD Connect를 사용 하 여 디렉터리 동기화의 새로운 동작입니다."
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
ms.openlocfilehash: e27dcbf9d71f83fa9566cae2fd99350297d1cd9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="identity-synchronization-and-duplicate-attribute-resiliency"></a><span data-ttu-id="bbb9a-103">ID 동기화 및 중복 특성 복원력</span><span class="sxs-lookup"><span data-stu-id="bbb9a-103">Identity synchronization and duplicate attribute resiliency</span></span>
<span data-ttu-id="bbb9a-104">중복 특성 복원력은 Microsoft의 동기화 도구 중 하나를 실행하는 경우 **UserPrincipalName** 및 **ProxyAddress**의 충돌로 발생하는 마찰을 제거하는 Azure Active Directory의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-104">Duplicate Attribute Resiliency is a feature in Azure Active Directory that will eliminate friction caused by **UserPrincipalName** and **ProxyAddress** conflicts when running one of Microsoft’s synchronization tools.</span></span>

<span data-ttu-id="bbb9a-105">이 두 특성은 모두에서 일반적으로 필요한 toobe 고유 **사용자**, **그룹**, 또는 **연락처** 지정된 Azure Active Directory 테 넌 트의 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-105">These two attributes are generally required toobe unique across all **User**, **Group**, or **Contact** objects in a given Azure Active Directory tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="bbb9a-106">사용자만 UPN을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-106">Only Users can have UPNs.</span></span>
> 
> 

<span data-ttu-id="bbb9a-107">이 기능을 사용 하는 새로운 동작 hello hello 동기화 파이프라인의 hello 클라우드 부분에 있으면 클라이언트 알 수 없는 및 Azure AD Connect, 디렉터리 동기화 및 MIM + 커넥터를 포함 하 여 Microsoft 동기화 제품에 대 한 관련 되므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-107">hello new behavior that this feature enables is in hello cloud portion of hello sync pipeline, therefore it is client agnostic and relevant for any Microsoft synchronization product including Azure AD Connect, DirSync and MIM + Connector.</span></span> <span data-ttu-id="bbb9a-108">hello 일반 용어 "동기화 클라이언트"는이 문서 toorepresent 이러한 제품 중 하나에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-108">hello generic term “sync client” is used in this document toorepresent any one of these products.</span></span>

## <a name="current-behavior"></a><span data-ttu-id="bbb9a-109">현재 동작</span><span class="sxs-lookup"><span data-stu-id="bbb9a-109">Current behavior</span></span>
<span data-ttu-id="bbb9a-110">가 시도 tooprovision이 고유성 제약 조건을 위반 하는 UPN 또는 / / ProxyAddress 값으로 새 개체를 Azure Active Directory는 해당 개체를 만들지를 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-110">If there is an attempt tooprovision a new object with a UPN or ProxyAddress value that violates this uniqueness constraint, Azure Active Directory blocks that object from being created.</span></span> <span data-ttu-id="bbb9a-111">마찬가지로, 고유 하지 않은 UPN 또는 / / ProxyAddress 개체 업데이트 되 면 hello 업데이트가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-111">Similarly, if an object is updated with a non-unique UPN or ProxyAddress, hello update fails.</span></span> <span data-ttu-id="bbb9a-112">시도 업데이트를 프로 비전 하는 hello 각 내보내기 주기 시 hello 동기화 클라이언트에서 다시 시도 되 고 toofail hello 충돌이 해결 될 때까지 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-112">hello provisioning attempt or update is retried by hello sync client upon each export cycle, and continues toofail until hello conflict is resolved.</span></span> <span data-ttu-id="bbb9a-113">각 시도 시 생성 되는 오류 보고서 전자 메일 및 hello 동기화 클라이언트에서 오류가 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-113">An error report email is generated upon each attempt and an error is logged by hello sync client.</span></span>

## <a name="behavior-with-duplicate-attribute-resiliency"></a><span data-ttu-id="bbb9a-114">중복 특성 복원력으로 동작</span><span class="sxs-lookup"><span data-stu-id="bbb9a-114">Behavior with Duplicate Attribute Resiliency</span></span>
<span data-ttu-id="bbb9a-115">완전히 대신 tooprovision 실패 하거나 중복 된 특성으로 Azure Active Directory "를 선택 하면" hello 고유성 제약 조건을 위반 하 게 hello 중복 된 특성 개체를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-115">Instead of completely failing tooprovision or update an object with a duplicate attribute, Azure Active Directory “quarantines” hello duplicate attribute which would violate hello uniqueness constraint.</span></span> <span data-ttu-id="bbb9a-116">이 특성에 필요한 경우 프로 비전, UserPrincipalName, 같은 hello 서비스 자리 표시자 값을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-116">If this attribute is required for provisioning, like UserPrincipalName, hello service assigns a placeholder value.</span></span> <span data-ttu-id="bbb9a-117">이러한 임시 값의 hello 형식은</span><span class="sxs-lookup"><span data-stu-id="bbb9a-117">hello format of these temporary values is</span></span>  
<span data-ttu-id="bbb9a-118">“***<OriginalPrefix>+<4DigitNumber>@<InitialTenantDomain>.onmicrosoft.com***”.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-118">“***<OriginalPrefix>+<4DigitNumber>@<InitialTenantDomain>.onmicrosoft.com***”.</span></span>  
<span data-ttu-id="bbb9a-119">다음과 같은 hello 특성이 필요 하지 않은 경우는 **/ / ProxyAddress**, Azure Active Directory 단순히 hello 충돌 특성을 격리 하 고 hello 개체 만들기 또는 업데이트를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-119">If hello attribute is not required, like a  **ProxyAddress**, Azure Active Directory simply quarantines hello conflict attribute and proceeds with hello object creation or update.</span></span>

<span data-ttu-id="bbb9a-120">Hello 특성을 격리 시 hello 충돌에 대 한 정보 hello 이전 동작에 사용 되는 동일한 오류 보고서를 전자 메일 hello에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-120">Upon quarantining hello attribute, information about hello conflict is sent in hello same error report email used in hello old behavior.</span></span> <span data-ttu-id="bbb9a-121">그러나이 정보에만 나타납니다 hello 오류 보고서에 한 번 발생 하는 hello 격리 하는 경우 것 중지 toobe 기록 나중에 전자 메일 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-121">However, this info only appears in hello error report one time, when hello quarantine happens, it does not continue toobe logged in future emails.</span></span> <span data-ttu-id="bbb9a-122">또한이 개체에 대 한 hello 내보내기에 성공 하면 이후 hello 동기화 클라이언트 오류를 기록 하지 않습니다 하 고는 hello를 다시 시도 하지 만들기 / 업데이트 작업을 다음 동기화 주기 시.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-122">Also, since hello export for this object has succeeded, hello sync client does not log an error and does not retry hello create / update operation upon subsequent sync cycles.</span></span>

<span data-ttu-id="bbb9a-123">이 문제는 새 특성 되었습니다 toosupport toohello 사용자, 그룹 및 연락처 개체 클래스를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-123">toosupport this behavior a new attribute has been added toohello User, Group, and Contact object classes:</span></span>  
<span data-ttu-id="bbb9a-124">**DirSyncProvisioningError**</span><span class="sxs-lookup"><span data-stu-id="bbb9a-124">**DirSyncProvisioningErrors**</span></span>

<span data-ttu-id="bbb9a-125">위반 하는 hello 고유성 제약 조건을 추가 해야 정상적으로 사용 되는 toostore hello 충돌 하는 특성이 있는 다중 값된 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-125">This is a multi-valued attribute that is used toostore hello conflicting attributes that would violate hello uniqueness constraint should they be added normally.</span></span> <span data-ttu-id="bbb9a-126">백그라운드 타이머 작업에 대 한 중복 된 특성 충돌 해결 및 격리를 통해 문제의 hello 특성을 자동으로 제거 하는 모든 시간 toolook를 실행 하는 Azure Active Directory에 설정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-126">A background timer task has been enabled in Azure Active Directory that  runs every hour toolook for duplicate attribute conflicts that have been resolved, and automatically removes hello attributes in question from quarantine.</span></span>

### <a name="enabling-duplicate-attribute-resiliency"></a><span data-ttu-id="bbb9a-127">중복 특성 복원력 활성화</span><span class="sxs-lookup"><span data-stu-id="bbb9a-127">Enabling Duplicate Attribute Resiliency</span></span>
<span data-ttu-id="bbb9a-128">중복 특성 복원 력 모든 Azure Active Directory 테 넌 트 간에 hello 새로운 기본 동작을 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-128">Duplicate Attribute Resiliency will be hello new default behavior across all Azure Active Directory tenants.</span></span> <span data-ttu-id="bbb9a-129">2016 년 8 월 22 일 년 이후에 처음으로 hello에 대 한 동기화를 사용 하도록 설정 된 모든 테 넌 트에 대해 기본적으로에 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-129">It will be on by default for all tenants that enabled synchronization for hello first time on August 22nd, 2016 or later.</span></span> <span data-ttu-id="bbb9a-130">동기화 이전 toothis 날짜를 사용 하도록 설정 된 테 넌 트 hello 기능 일괄 처리에서 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-130">Tenants that enabled sync prior toothis date will have hello feature enabled in batches.</span></span> <span data-ttu-id="bbb9a-131">2016 년 9 월에에서 시작 됩니다.이 출시 및 tooeach 테 넌 트의 기술 알림 접촉이 hello 특정 날짜 hello 기능을 설정할 때 전자 메일 알림이 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-131">This rollout will begin in September 2016, and an email notification will be sent tooeach tenant's technical notification contact with hello specific date when hello feature will be enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="bbb9a-132">중복 특성 복원력이 설정된 후에는 해제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-132">Once Duplicate Attribute Resiliency has been turned on it cannot be disabled.</span></span>

<span data-ttu-id="bbb9a-133">테 넌 트에 대 한 hello 기능이 활성화 된 경우 toocheck, 후 그렇게 hello hello Azure Active Directory PowerShell 모듈의 최신 버전을 다운로드 및 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="bbb9a-133">toocheck if hello feature is enabled for your tenant, you can do so by downloading hello latest version of hello Azure Active Directory PowerShell module and running:</span></span>

`Get-MsolDirSyncFeatures -Feature DuplicateUPNResiliency`

`Get-MsolDirSyncFeatures -Feature DuplicateProxyAddressResiliency`

> [!NOTE]
> <span data-ttu-id="bbb9a-134">테 넌 트에 대해 켜져 전에 집합 MsolDirSyncFeature cmdlet tooproactively hello 중복 특성 탄력성 기능을 사용을 더 이상 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-134">You can no longer use Set-MsolDirSyncFeature cmdlet tooproactively enable hello Duplicate Attribute Resiliency feature before it is turned on for your tenant.</span></span> <span data-ttu-id="bbb9a-135">toobe 수 tootest hello 기능을 새 Azure Active Directory 테 넌 트 toocreate가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-135">toobe able tootest hello feature, you will need toocreate a new Azure Active Directory tenant.</span></span>

## <a name="identifying-objects-with-dirsyncprovisioningerrors"></a><span data-ttu-id="bbb9a-136">DirSyncProvisioningErrors로 개체 식별</span><span class="sxs-lookup"><span data-stu-id="bbb9a-136">Identifying Objects with DirSyncProvisioningErrors</span></span>
<span data-ttu-id="bbb9a-137">Tooduplicate 속성 충돌, PowerShell Azure Active Directory 및 Office 365 관리 포털 hello 인해 이러한 오류가 있는 tooidentify 개체는 현재 두 가지 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-137">There are currently two methods tooidentify objects that have these errors due tooduplicate property conflicts, Azure Active Directory PowerShell and hello Office 365 Admin Portal.</span></span> <span data-ttu-id="bbb9a-138">계획 tooextend tooadditional 포털 기반 보고 hello 앞에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-138">There are plans tooextend tooadditional portal based reporting in hello future.</span></span>

### <a name="azure-active-directory-powershell"></a><span data-ttu-id="bbb9a-139">Azure Active Directory PowerShell</span><span class="sxs-lookup"><span data-stu-id="bbb9a-139">Azure Active Directory PowerShell</span></span>
<span data-ttu-id="bbb9a-140">이 항목의 PowerShell cmdlet hello에 대 한 hello 다음은 true입니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-140">For hello PowerShell cmdlets in this topic, hello following is true:</span></span>

* <span data-ttu-id="bbb9a-141">Cmdlet을 다음 hello 모두 대/소문자 구분입니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-141">All of hello following cmdlets are case sensitive.</span></span>
* <span data-ttu-id="bbb9a-142">hello **– ErrorCategory PropertyConflict** 항상 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-142">hello **–ErrorCategory PropertyConflict** must always be included.</span></span> <span data-ttu-id="bbb9a-143">다른 종류의 현재는 **ErrorCategory**, 하지만 hello 향후에 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-143">There are currently no other types of **ErrorCategory**, but this may be extended in hello future.</span></span>

<span data-ttu-id="bbb9a-144">먼저 **Connect-MsolService**를 실행하고 테넌트 관리자에 대한 자격 증명을 입력하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-144">First, get started by running **Connect-MsolService** and entering credentials for a tenant administrator.</span></span>

<span data-ttu-id="bbb9a-145">그런 다음 다른 방법으로 다음 cmdlet과 연산자에 해당 하는 tooview의 오류 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-145">Then, use hello following cmdlets and operators tooview errors in different ways:</span></span>

1. [<span data-ttu-id="bbb9a-146">모두 표시</span><span class="sxs-lookup"><span data-stu-id="bbb9a-146">See All</span></span>](#see-all)
2. [<span data-ttu-id="bbb9a-147">속성 형식으로</span><span class="sxs-lookup"><span data-stu-id="bbb9a-147">By Property Type</span></span>](#by-property-type)
3. [<span data-ttu-id="bbb9a-148">충돌 값으로</span><span class="sxs-lookup"><span data-stu-id="bbb9a-148">By Conflicting Value</span></span>](#by-conflicting-value)
4. [<span data-ttu-id="bbb9a-149">문자열 검색을 사용하여</span><span class="sxs-lookup"><span data-stu-id="bbb9a-149">Using a String Search</span></span>](#using-a-string-search)
5. [<span data-ttu-id="bbb9a-150">정렬</span><span class="sxs-lookup"><span data-stu-id="bbb9a-150">Sorted</span></span>](#sorted)
6. [<span data-ttu-id="bbb9a-151">제한된 수량 또는 모두</span><span class="sxs-lookup"><span data-stu-id="bbb9a-151">In a Limited Quantity or All</span></span>](#in-a-limited-quantity-or-all)

#### <a name="see-all"></a><span data-ttu-id="bbb9a-152">모두 표시</span><span class="sxs-lookup"><span data-stu-id="bbb9a-152">See all</span></span>
<span data-ttu-id="bbb9a-153">연결 되 면 toosee 일반 프로 비전 오류 hello 테 넌 트에 특성 목록을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-153">Once connected, toosee a general list of attribute provisioning errors in hello tenant run:</span></span>

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict`

<span data-ttu-id="bbb9a-154">이 hello 다음과 같은 결과 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-154">This produces a result like hello following:</span></span>  
 <span data-ttu-id="bbb9a-155">![Get MsolDirSyncProvisioningError](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1.png "Get MsolDirSyncProvisioningError")</span><span class="sxs-lookup"><span data-stu-id="bbb9a-155">![Get-MsolDirSyncProvisioningError](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1.png "Get-MsolDirSyncProvisioningError")</span></span>  

#### <a name="by-property-type"></a><span data-ttu-id="bbb9a-156">속성 형식으로</span><span class="sxs-lookup"><span data-stu-id="bbb9a-156">By property type</span></span>
<span data-ttu-id="bbb9a-157">속성 형식에 의해 toosee 오류 추가 hello **-PropertyName** hello로 플래그 **UserPrincipalName** 또는 **ProxyAddresses** 인수:</span><span class="sxs-lookup"><span data-stu-id="bbb9a-157">toosee errors by property type, add hello **-PropertyName** flag with hello **UserPrincipalName** or **ProxyAddresses** argument:</span></span>

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName UserPrincipalName`

<span data-ttu-id="bbb9a-158">또는</span><span class="sxs-lookup"><span data-stu-id="bbb9a-158">Or</span></span>

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName ProxyAddresses`

#### <a name="by-conflicting-value"></a><span data-ttu-id="bbb9a-159">충돌 값으로</span><span class="sxs-lookup"><span data-stu-id="bbb9a-159">By conflicting value</span></span>
<span data-ttu-id="bbb9a-160">toosee 오류 tooa 특정 속성을 관련 된 추가 hello **-PropertyValue** 플래그 (**-PropertyName** 이 플래그를 추가 하는 경우 함께 사용 해야 합니다).</span><span class="sxs-lookup"><span data-stu-id="bbb9a-160">toosee errors relating tooa specific property add hello **-PropertyValue** flag (**-PropertyName** must be used as well when adding this flag):</span></span>

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyValue User@domain.com -PropertyName UserPrincipalName`

#### <a name="using-a-string-search"></a><span data-ttu-id="bbb9a-161">문자열 검색을 사용하여</span><span class="sxs-lookup"><span data-stu-id="bbb9a-161">Using a string search</span></span>
<span data-ttu-id="bbb9a-162">hello를 사용 하는 광범위 한 문자열 검색 toodo **-SearchString** 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-162">toodo a broad string search use hello **-SearchString** flag.</span></span> <span data-ttu-id="bbb9a-163">이 사용할 수 독립적으로 모든 플래그의 hello 예외와 함께 위의 hello **-ErrorCategory PropertyConflict**는 항상 필요한 것은:</span><span class="sxs-lookup"><span data-stu-id="bbb9a-163">This can be used independently from all of hello above flags, with hello exception of **-ErrorCategory PropertyConflict**, which is always required:</span></span>

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -SearchString User`

#### <a name="in-a-limited-quantity-or-all"></a><span data-ttu-id="bbb9a-164">제한된 수량 또는 모두</span><span class="sxs-lookup"><span data-stu-id="bbb9a-164">In a limited quantity or all</span></span>
1. <span data-ttu-id="bbb9a-165">**MaxResults <Int>**  수 toolimit hello 쿼리 tooa 특정 수의 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-165">**MaxResults <Int>** can be used toolimit hello query tooa specific number of values.</span></span>
2. <span data-ttu-id="bbb9a-166">**모든** 사용된 tooensure 오류가 많이 있는 경우 모두 hello 모든 결과 검색 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-166">**All** can be used tooensure all results are retrieved in hello case that a large number of errors exists.</span></span>

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -MaxResults 5`

## <a name="office-365-admin-portal"></a><span data-ttu-id="bbb9a-167">Office 365 관리 포털</span><span class="sxs-lookup"><span data-stu-id="bbb9a-167">Office 365 admin portal</span></span>
<span data-ttu-id="bbb9a-168">Hello Office 365 관리 센터에서 디렉터리 동기화 오류를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-168">You can view directory synchronization errors in hello Office 365 admin center.</span></span> <span data-ttu-id="bbb9a-169">hello Office 365 포털만 화면에서 보고서를 hello **사용자** 이러한 오류가 있는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-169">hello report in hello Office 365 portal only displays **User** objects that have these errors.</span></span> <span data-ttu-id="bbb9a-170">**그룹** 및 **연락처** 간의 충돌에 대한 정보는 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-170">It does not show info about conflicts between **Groups** and **Contacts**.</span></span>

<span data-ttu-id="bbb9a-171">![활성 사용자](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1234.png "활성 사용자")</span><span class="sxs-lookup"><span data-stu-id="bbb9a-171">![Active Users](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1234.png "Active Users")</span></span>

<span data-ttu-id="bbb9a-172">Admin 님 안녕하세요 Office 365에서에서 디렉터리 동기화 오류 tooview 센터 방법에 지침은 [Office 365의 디렉터리 동기화 오류를 식별](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067)합니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-172">For instructions on how tooview directory synchronization errors in hello Office 365 admin center, see [Identify directory synchronization errors in Office 365](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067).</span></span>

### <a name="identity-synchronization-error-report"></a><span data-ttu-id="bbb9a-173">ID 동기화 오류 보고서</span><span class="sxs-lookup"><span data-stu-id="bbb9a-173">Identity synchronization error report</span></span>
<span data-ttu-id="bbb9a-174">충돌 하는 중복 된 특성을 가진 개체에 포함 된 알림을이 새로운 동작으로 처리 될 때 Identity 동기화 오류 보고서에 전자 메일로 보낼 hello 표준 toohello 기술 알림 연락처 hello 테 넌 트에 대 한 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-174">When an object with a duplicate attribute conflict is handled with this new behavior a notification is included in hello standard Identity Synchronization Error Report email that is sent toohello Technical Notification contact for hello tenant.</span></span> <span data-ttu-id="bbb9a-175">그러나 이 동작에서 중요한 변경 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-175">However, there is an important change in this behavior.</span></span> <span data-ttu-id="bbb9a-176">Hello 지난에 중복 된 특성 충돌에 대 한 정보 hello 충돌이 해결 될 때까지 모든 후속 오류 보고서에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-176">In hello past, information about a duplicate attribute conflict would be included in every subsequent error report until hello conflict was resolved.</span></span> <span data-ttu-id="bbb9a-177">이 새로운 동작으로 지정 된 충돌에 대 한 hello 오류 알림 않습니다에 표시 한 번-hello 시간 hello 충돌 하는 특성 격리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-177">With this new behavior, hello error notification for a given conflict does only appear once- at hello time hello conflicting attribute is quarantined.</span></span>

<span data-ttu-id="bbb9a-178">모양의 어떤 hello 전자 메일 알림 / / ProxyAddress 충돌에 대 한 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-178">Here is an example of what hello email notification looks like for a ProxyAddress conflict:</span></span>  
    <span data-ttu-id="bbb9a-179">![활성 사용자](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "활성 사용자")</span><span class="sxs-lookup"><span data-stu-id="bbb9a-179">![Active Users](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "Active Users")</span></span>  

## <a name="resolving-conflicts"></a><span data-ttu-id="bbb9a-180">충돌 해결</span><span class="sxs-lookup"><span data-stu-id="bbb9a-180">Resolving conflicts</span></span>
<span data-ttu-id="bbb9a-181">이러한 오류에 대 한 전략 및 해결 방법을 문제를 해결 하지 다를 수는 hello 방식 hello 지난 오류 중복 된 특성을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-181">Troubleshooting strategy and resolution tactics for these errors should not differ from hello way duplicate attribute errors were handled in hello past.</span></span> <span data-ttu-id="bbb9a-182">hello 유일한 차이점은 hello 충돌을 해결 되 면 hello 테 넌 트 서비스 측 tooautomatically hello 통해 hello 타이머 작업 스윕의 질문 toohello 적절 한 개체에 hello 특성 추가 한다는 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-182">hello only difference is that hello timer task sweeps through hello tenant on hello service-side tooautomatically add hello attribute in question toohello proper object once hello conflict is resolved.</span></span>

<span data-ttu-id="bbb9a-183">hello 다음 문서에 간략하게 설명 다양 한 문제 해결 및 해결 방법: [중복 되거나 잘못 된 특성에는 Office 365의 디렉터리 동기화 되지 않게](https://support.microsoft.com/kb/2647098)합니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-183">hello following article outlines various troubleshooting and resolution strategies: [Duplicate or invalid attributes prevent directory synchronization in Office 365](https://support.microsoft.com/kb/2647098).</span></span>

## <a name="known-issues"></a><span data-ttu-id="bbb9a-184">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="bbb9a-184">Known issues</span></span>
<span data-ttu-id="bbb9a-185">이러한 알려진 문제로 인해 데이터 손실 또는 서비스 저하가 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-185">None of these known issues causes data loss or service degradation.</span></span> <span data-ttu-id="bbb9a-186">그 중 일부는 미적인 따라서는 다른 표준 "*사전 복원 력*" 중복 된 특성 오류 toobe hello 충돌 특성을 포함 하며 다른 격리 대신 throw 하면 특정 오류 toorequire 추가 수동 픽스업 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-186">Several of them are aesthetic, others cause standard “*pre-resiliency*” duplicate attribute errors toobe thrown instead of quarantining hello conflict attribute, and another causes certain errors toorequire extra manual fix-up.</span></span>

<span data-ttu-id="bbb9a-187">**핵심 동작:**</span><span class="sxs-lookup"><span data-stu-id="bbb9a-187">**Core behavior:**</span></span>

1. <span data-ttu-id="bbb9a-188">특정 한 특성 구성 사용 하 여 개체 격리 되 고 중복 된 것과 반대로 toohello 특성으로 tooreceive 내보내기 오류를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-188">Objects with specific attribute configurations continue tooreceive export errors as opposed toohello duplicate attribute(s) being quarantined.</span></span>  
   <span data-ttu-id="bbb9a-189">예:</span><span class="sxs-lookup"><span data-stu-id="bbb9a-189">For example:</span></span>
   
    <span data-ttu-id="bbb9a-190">a.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-190">a.</span></span> <span data-ttu-id="bbb9a-191">새로운 사용자가 **Joe@contoso.com**의 UPN과 ProxyAddress **smtp:Joe@contoso.com**로 AD에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-191">New user is created in AD with a UPN of **Joe@contoso.com** and ProxyAddress **smtp:Joe@contoso.com**</span></span>
   
    <span data-ttu-id="bbb9a-192">b.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-192">b.</span></span> <span data-ttu-id="bbb9a-193">hello이 개체의 속성 충돌할 ProxyAddress 인 기존 그룹  **SMTP:Joe@contoso.com** 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-193">hello properties of this object conflict with an existing Group, where ProxyAddress is **SMTP:Joe@contoso.com**.</span></span>
   
    <span data-ttu-id="bbb9a-194">c.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-194">c.</span></span> <span data-ttu-id="bbb9a-195">을 내보낼 때는 **/ / ProxyAddress 충돌** hello 충돌 특성 격리 하지 않고 오류가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-195">Upon export, a **ProxyAddress conflict** error is thrown instead of having hello conflict attributes quarantined.</span></span> <span data-ttu-id="bbb9a-196">hello 복원 력 기능은 사용 하기 전에 것 처럼 각 다음 동기화 주기 시 hello 작업이 다시 시도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-196">hello operation is retried upon each subsequent sync cycle, as it would have been before hello resiliency feature was enabled.</span></span>
2. <span data-ttu-id="bbb9a-197">두 개의 그룹이 생성 되는 경우 온-프레미스 hello로 동일 SMTP 주소, 중복 되는 표준 hello 첫 번째 시도에 실패 한 tooprovision **/ / ProxyAddress** 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-197">If two Groups are created on-premises with hello same SMTP address, one fails tooprovision on hello first attempt with a standard duplicate **ProxyAddress** error.</span></span> <span data-ttu-id="bbb9a-198">그러나 hello 중복 값은 제대로 격리 hello 시 다음 동기화 주기.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-198">However, hello duplicate value is properly quarantined upon hello next sync cycle.</span></span>

<span data-ttu-id="bbb9a-199">**Office 포털 보고서**:</span><span class="sxs-lookup"><span data-stu-id="bbb9a-199">**Office Portal Report**:</span></span>

1. <span data-ttu-id="bbb9a-200">UPN 충돌 집합에서 두 개체에 대 한 hello 자세한 오류 메시지는 동일한 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-200">hello detailed error message for two objects in a UPN conflict set is hello same.</span></span> <span data-ttu-id="bbb9a-201">이는 실제로 하나에만 변경된 데이터가 있는 경우 둘 모두 해당 UPN을 변경 / 격리했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-201">This indicates that they have both had their UPN changed / quarantined, when in fact only a one of them had any data changed.</span></span>
2. <span data-ttu-id="bbb9a-202">UPN 충돌에 대 한 hello 자세한 오류 메시지에는 해당 UPN 변경/격리는 사용자에 대 한 잘못 된 displayName hello 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-202">hello detailed error message for a UPN conflict shows hello wrong displayName for a user who has had their UPN changed/quarantined.</span></span> <span data-ttu-id="bbb9a-203">예:</span><span class="sxs-lookup"><span data-stu-id="bbb9a-203">For example:</span></span>
   
    <span data-ttu-id="bbb9a-204">a.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-204">a.</span></span> <span data-ttu-id="bbb9a-205">**사용자 A**는 먼저 **UPN = User@contoso.com**과 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-205">**User A** syncs up first with **UPN = User@contoso.com**.</span></span>
   
    <span data-ttu-id="bbb9a-206">b.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-206">b.</span></span> <span data-ttu-id="bbb9a-207">**사용자 B** 가 된 다음 동기화 시도 toobe **UPN = User@contoso.com** 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-207">**User B** is attempted toobe synced up next with **UPN = User@contoso.com**.</span></span>
   
    <span data-ttu-id="bbb9a-208">c.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-208">c.</span></span> <span data-ttu-id="bbb9a-209">**사용자 B의** UPN 너무 변경 **User1234@contoso.onmicrosoft.com**  및  **User@contoso.com**  너무 추가**DirSyncProvisioningErrors**합니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-209">**User B’s** UPN is changed too**User1234@contoso.onmicrosoft.com** and **User@contoso.com** is added too**DirSyncProvisioningErrors**.</span></span>
   
    <span data-ttu-id="bbb9a-210">d.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-210">d.</span></span> <span data-ttu-id="bbb9a-211">hello 오류 메시지에 대 한 **사용자 B** 나타나야 합니다 **사용자 A** 이미  **User@contoso.com**  UPN을 하지만 보듯이 **사용자 B의** 자체 표시 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-211">hello error message for **User B** should indicate that **User A** already has **User@contoso.com** as a UPN, but it shows **User B’s** own displayName.</span></span>

<span data-ttu-id="bbb9a-212">**ID 동기화 오류 보고서**:</span><span class="sxs-lookup"><span data-stu-id="bbb9a-212">**Identity synchronization error report**:</span></span>

<span data-ttu-id="bbb9a-213">에 대 한 hello 링크 *방법과 관련 된 단계 tooresolve이이 문제* 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-213">hello link for *steps on how tooresolve this issue* is incorrect:</span></span>  
    <span data-ttu-id="bbb9a-214">![활성 사용자](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "활성 사용자")</span><span class="sxs-lookup"><span data-stu-id="bbb9a-214">![Active Users](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "Active Users")</span></span>  

<span data-ttu-id="bbb9a-215">너무 가리켜야[https://aka.ms/duplicateattributeresiliency](https://aka.ms/duplicateattributeresiliency)합니다.</span><span class="sxs-lookup"><span data-stu-id="bbb9a-215">It should point too[https://aka.ms/duplicateattributeresiliency](https://aka.ms/duplicateattributeresiliency).</span></span>

## <a name="see-also"></a><span data-ttu-id="bbb9a-216">참고 항목</span><span class="sxs-lookup"><span data-stu-id="bbb9a-216">See also</span></span>
* [<span data-ttu-id="bbb9a-217">Azure AD Connect 동기화</span><span class="sxs-lookup"><span data-stu-id="bbb9a-217">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="bbb9a-218">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="bbb9a-218">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
* [<span data-ttu-id="bbb9a-219">Office 365에서 디렉터리 동기화 오류 확인</span><span class="sxs-lookup"><span data-stu-id="bbb9a-219">Identify directory synchronization errors in Office 365</span></span>](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067)

