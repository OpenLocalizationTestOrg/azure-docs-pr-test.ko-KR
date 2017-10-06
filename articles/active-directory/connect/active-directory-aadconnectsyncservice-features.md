---
title: "aaaAzure AD Connect 동기화 서비스 기능 및 구성 | Microsoft Docs"
description: "Azure AD Connect 동기화 서비스의 서비스 쪽 기능을 설명합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 213aab20-0a61-434a-9545-c4637628da81
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 7ad05c45bb6b5fd5deaa3466e2936b19d3d9eabb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-features"></a><span data-ttu-id="12341-103">Azure AD Connect 동기화 서비스 기능</span><span class="sxs-lookup"><span data-stu-id="12341-103">Azure AD Connect sync service features</span></span>
<span data-ttu-id="12341-104">Azure AD Connect의 hello 동기화 기능에는 두 가지 구성 요소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12341-104">hello synchronization feature of Azure AD Connect has two components:</span></span>

* <span data-ttu-id="12341-105">hello 온-프레미스 구성 요소 라는 **Azure AD Connect 동기화**라고도 **동기화 엔진이**합니다.</span><span class="sxs-lookup"><span data-stu-id="12341-105">hello on-premises component named **Azure AD Connect sync**, also called **sync engine**.</span></span>
* <span data-ttu-id="12341-106">Azure ad에서로 알려져 있는 hello 서비스 **Azure AD Connect 동기화 서비스**</span><span class="sxs-lookup"><span data-stu-id="12341-106">hello service residing in Azure AD also known as **Azure AD Connect sync service**</span></span>

<span data-ttu-id="12341-107">이 항목에서는 다음 hello 기능이 하는 방법에 대해 설명의 hello **Azure AD Connect 동기화 서비스** 작업 및 방법 Windows PowerShell을 사용 하 여 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12341-107">This topic explains how hello following features of hello **Azure AD Connect sync service** work and how you can configure them using Windows PowerShell.</span></span>

<span data-ttu-id="12341-108">이러한 설정을 hello 구성 [Azure Active Directory에 대 한 Windows PowerShell 모듈](http://aka.ms/aadposh)합니다.</span><span class="sxs-lookup"><span data-stu-id="12341-108">These settings are configured by hello [Azure Active Directory Module for Windows PowerShell](http://aka.ms/aadposh).</span></span> <span data-ttu-id="12341-109">Azure AD Connect에서 다운로드하여 별도로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="12341-109">Download and install it separately from Azure AD Connect.</span></span> <span data-ttu-id="12341-110">이 항목에서 설명 하는 hello cmdlet hello에 도입 된 [2016 년 3 월 릴리스 (빌드 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1)합니다.</span><span class="sxs-lookup"><span data-stu-id="12341-110">hello cmdlets documented in this topic were introduced in hello [2016 March release (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span></span> <span data-ttu-id="12341-111">이 항목에서 설명 하는 hello cmdlet 없는 또는 결과 동일 하 고 있는지 확인 하는 hello를 생성 하지 않는 경우 hello 최신 버전을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="12341-111">If you do not have hello cmdlets documented in this topic or they do not produce hello same result, then make sure you run hello latest version.</span></span>

<span data-ttu-id="12341-112">를 실행 하 여 Azure AD 디렉터리에서 toosee hello 구성 `Get-MsolDirSyncFeatures`합니다.</span><span class="sxs-lookup"><span data-stu-id="12341-112">toosee hello configuration in your Azure AD directory, run `Get-MsolDirSyncFeatures`.</span></span>  
<span data-ttu-id="12341-113">![Get-MsolDirSyncFeatures 결과](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span><span class="sxs-lookup"><span data-stu-id="12341-113">![Get-MsolDirSyncFeatures result](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span></span>

<span data-ttu-id="12341-114">이러한 설정 중 대부분은 Azure AD Connect에서만 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12341-114">Many of these settings can only be changed by Azure AD Connect.</span></span>

<span data-ttu-id="12341-115">hello 다음 설정을 구성할 수 있습니다 하 여 `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="12341-115">hello following settings can be configured by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="12341-116">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="12341-116">DirSyncFeature</span></span> | <span data-ttu-id="12341-117">주석</span><span class="sxs-lookup"><span data-stu-id="12341-117">Comment</span></span> |
| --- | --- |
| [<span data-ttu-id="12341-118">EnableSoftMatchOnUpn</span><span class="sxs-lookup"><span data-stu-id="12341-118">EnableSoftMatchOnUpn</span></span>](#userprincipalname-soft-match) |<span data-ttu-id="12341-119">또한 tooprimary SMTP 주소에 userPrincipalName에 개체 toojoin를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="12341-119">Allows objects toojoin on userPrincipalName in addition tooprimary SMTP address.</span></span> |
| [<span data-ttu-id="12341-120">SynchronizeUpnForManagedUsers</span><span class="sxs-lookup"><span data-stu-id="12341-120">SynchronizeUpnForManagedUsers</span></span>](#synchronize-userprincipalname-updates) |<span data-ttu-id="12341-121">(페더레이션 되지 않은) 사용자가 관리 되는 사용이 허가 hello 동기화 엔진 tooupdate hello userPrincipalName 특성을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="12341-121">Allows hello sync engine tooupdate hello userPrincipalName attribute for managed/licensed (non-federated) users.</span></span> |

<span data-ttu-id="12341-122">기능을 사용하도록 설정한 후 다시 해제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="12341-122">After you have enabled a feature, it cannot be disabled again.</span></span>

> [!NOTE]
> <span data-ttu-id="12341-123">2016 년 8 월 24 일에서 기능 hello *특성 복원 력 중복* 은 새로운 Azure에 대 한 기본값으로 사용 가능 AD 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="12341-123">From August 24, 2016 hello feature *Duplicate attribute resiliency* is enabled by default for new Azure AD directories.</span></span> <span data-ttu-id="12341-124">또한 이 기능은 이 날짜 이전에 생성된 디렉터리에서 롤아웃되고 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="12341-124">This feature will also be rolled out and enabled on directories created before this date.</span></span> <span data-ttu-id="12341-125">디렉터리가 있을 때 프로그램 tooget에 대 한이 기능 사용 전자 메일 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="12341-125">You will receive an email notification when your directory is about tooget this feature enabled.</span></span>
> 
> 

<span data-ttu-id="12341-126">hello 다음과 같은 Azure AD Connect에서 구성 된 설정과으로 수정할 수 없으며 `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="12341-126">hello following settings are configured by Azure AD Connect and cannot be modified by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="12341-127">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="12341-127">DirSyncFeature</span></span> | <span data-ttu-id="12341-128">주석</span><span class="sxs-lookup"><span data-stu-id="12341-128">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="12341-129">DeviceWriteback</span><span class="sxs-lookup"><span data-stu-id="12341-129">DeviceWriteback</span></span> |[<span data-ttu-id="12341-130">Azure AD Connect: 장치 쓰기 저장 사용</span><span class="sxs-lookup"><span data-stu-id="12341-130">Azure AD Connect: Enabling device writeback</span></span>](active-directory-aadconnect-feature-device-writeback.md) |
| <span data-ttu-id="12341-131">DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="12341-131">DirectoryExtensions</span></span> |[<span data-ttu-id="12341-132">Azure AD Connect 동기화: 디렉터리 확장</span><span class="sxs-lookup"><span data-stu-id="12341-132">Azure AD Connect sync: Directory extensions</span></span>](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [<span data-ttu-id="12341-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span><span class="sxs-lookup"><span data-stu-id="12341-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span></span>](#duplicate-attribute-resiliency) |<span data-ttu-id="12341-134">다른 개체 보다는 hello 전체 개체 내보내기 작업 중 실패의 중복 때 격리 하는 특성 toobe를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12341-134">Allows an attribute toobe quarantined when it is a duplicate of another object rather than failing hello entire object during export.</span></span> |
| <span data-ttu-id="12341-135">PasswordSync</span><span class="sxs-lookup"><span data-stu-id="12341-135">PasswordSync</span></span> |[<span data-ttu-id="12341-136">Azure AD Connect 동기화로 암호 동기화 구현</span><span class="sxs-lookup"><span data-stu-id="12341-136">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md) |
| <span data-ttu-id="12341-137">UnifiedGroupWriteback</span><span class="sxs-lookup"><span data-stu-id="12341-137">UnifiedGroupWriteback</span></span> |[<span data-ttu-id="12341-138">미리 보기: 그룹 쓰기 저장</span><span class="sxs-lookup"><span data-stu-id="12341-138">Preview: Group writeback</span></span>](active-directory-aadconnect-feature-preview.md#group-writeback) |
| <span data-ttu-id="12341-139">UserWriteback</span><span class="sxs-lookup"><span data-stu-id="12341-139">UserWriteback</span></span> |<span data-ttu-id="12341-140">현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12341-140">Not currently supported.</span></span> |

## <a name="duplicate-attribute-resiliency"></a><span data-ttu-id="12341-141">중복 특성 복원력</span><span class="sxs-lookup"><span data-stu-id="12341-141">Duplicate attribute resiliency</span></span>
<span data-ttu-id="12341-142">Tooprovision 실패 하는 대신 개체와 중복 된 Upn/proxyAddresses, hello 중복 된 특성은 "격리" 임시 값이 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12341-142">Instead of failing tooprovision objects with duplicate UPNs / proxyAddresses, hello duplicated attribute is “quarantined” and a temporary value is assigned.</span></span> <span data-ttu-id="12341-143">Hello 충돌이 해결 되 면 hello 임시 UPN은 toohello 적절 한 값을 자동으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="12341-143">When hello conflict is resolved, hello temporary UPN is changed toohello proper value automatically.</span></span> <span data-ttu-id="12341-144">자세한 내용은 [ID 동기화 및 중복 특성 복원력](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12341-144">For more details, see [Identity synchronization and duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="userprincipalname-soft-match"></a><span data-ttu-id="12341-145">UserPrincipalName 소프트 일치</span><span class="sxs-lookup"><span data-stu-id="12341-145">UserPrincipalName soft match</span></span>
<span data-ttu-id="12341-146">또한 toohello에서 소프트 일치 UPN에 대 한 사용이 기능을 사용 하는 경우 [기본 SMTP 주소](https://support.microsoft.com/kb/2641663), 항상 활성화 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12341-146">When this feature is enabled, soft-match is enabled for UPN in addition toohello [primary SMTP address](https://support.microsoft.com/kb/2641663), which is always enabled.</span></span> <span data-ttu-id="12341-147">소프트-일치가 toomatch 사용 되는 기존 클라우드 사용자가 온-프레미스 사용자와 Azure AD에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="12341-147">Soft-match is used toomatch existing cloud users in Azure AD with on-premises users.</span></span>

<span data-ttu-id="12341-148">필요한 toomatch 온-프레미스 AD 계정 hello 클라우드에서 만든 계정 가진 Exchange Online을 사용 하지 않는 경우이 기능은 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="12341-148">If you need toomatch on-premises AD accounts with existing accounts created in hello cloud and you are not using Exchange Online, then this feature is useful.</span></span> <span data-ttu-id="12341-149">이 시나리오에서는 일반적으로 설명 tooset hello SMTP 특성에에서 없는 hello 클라우드입니다.</span><span class="sxs-lookup"><span data-stu-id="12341-149">In this scenario, you generally don’t have a reason tooset hello SMTP attribute in hello cloud.</span></span>

<span data-ttu-id="12341-150">이 기능은 새로 만든 Azure AD 디렉터리에 기본적으로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12341-150">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="12341-151">다음을 실행하여 이 기능을 사용하도록 설정했는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12341-151">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

<span data-ttu-id="12341-152">Azure AD 디렉터리에서 이 기능을 사용하도록 설정하지 않은 경우 다음을 실행하여 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12341-152">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a><span data-ttu-id="12341-153">UserPrincipalName 업데이트 동기화</span><span class="sxs-lookup"><span data-stu-id="12341-153">Synchronize userPrincipalName updates</span></span>
<span data-ttu-id="12341-154">지금까지 온-프레미스에서 hello 동기화 서비스를 사용 하 여 업데이트 toohello UserPrincipalName 특성에 차단 된 이러한 조건을 모두 true가 아니면:</span><span class="sxs-lookup"><span data-stu-id="12341-154">Historically, updates toohello UserPrincipalName attribute using hello sync service from on-premises has been blocked, unless both of these conditions are true:</span></span>

* <span data-ttu-id="12341-155">hello 사용자 (페더레이션 되지 않은)으로 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12341-155">hello user is managed (non-federated).</span></span>
* <span data-ttu-id="12341-156">hello 사용자 라이선스를 할당 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="12341-156">hello user has not been assigned a license.</span></span>

<span data-ttu-id="12341-157">자세한 내용은 참조 하십시오. [온-프레미스 UPN 또는 대체 로그인 ID 사용자를 Office 365, Azure 또는 Intune 이름이 일치 하지 않습니다 hello](https://support.microsoft.com/kb/2523192)합니다.</span><span class="sxs-lookup"><span data-stu-id="12341-157">For more details, see [User names in Office 365, Azure, or Intune don't match hello on-premises UPN or alternate login ID](https://support.microsoft.com/kb/2523192).</span></span>

<span data-ttu-id="12341-158">이 기능을 사용 하면 변경 된 온-프레미스 되 고 암호 동기화를 사용 하 여 hello 동기화 엔진 tooupdate hello userPrincipalName가 있습니다. 페더레이션을 사용하는 경우 이 기능은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12341-158">Enabling this feature allows hello sync engine tooupdate hello userPrincipalName when it is changed on-premises and you use password sync. If you use federation, this feature is not supported.</span></span>

<span data-ttu-id="12341-159">이 기능은 새로 만든 Azure AD 디렉터리에 기본적으로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12341-159">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="12341-160">다음을 실행하여 이 기능을 사용하도록 설정했는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12341-160">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

<span data-ttu-id="12341-161">Azure AD 디렉터리에서 이 기능을 사용하도록 설정하지 않은 경우 다음을 실행하여 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12341-161">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

<span data-ttu-id="12341-162">이 기능을 사용하도록 설정하면 기존 userPrincipalName 값이 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="12341-162">After enabling this feature, existing userPrincipalName values will remain as-is.</span></span> <span data-ttu-id="12341-163">사용자에 게 hello 일반 델타 동기화는 hello userPrincipalName 특성 온-프레미스의 다음 변경 시 hello UPN을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="12341-163">On next change of hello userPrincipalName attribute on-premises, hello normal delta sync on users will update hello UPN.</span></span>  

## <a name="see-also"></a><span data-ttu-id="12341-164">참고 항목</span><span class="sxs-lookup"><span data-stu-id="12341-164">See also</span></span>
* [<span data-ttu-id="12341-165">Azure AD Connect 동기화</span><span class="sxs-lookup"><span data-stu-id="12341-165">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="12341-166">[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)</span><span class="sxs-lookup"><span data-stu-id="12341-166">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

