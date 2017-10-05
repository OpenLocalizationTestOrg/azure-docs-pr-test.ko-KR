---
title: "Azure AD Connect 동기화 서비스 기능 및 구성 | Microsoft Docs"
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
ms.openlocfilehash: c2873510c280a2683c235cfdce3d2617c3b665cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-service-features"></a><span data-ttu-id="1c3d6-103">Azure AD Connect 동기화 서비스 기능</span><span class="sxs-lookup"><span data-stu-id="1c3d6-103">Azure AD Connect sync service features</span></span>
<span data-ttu-id="1c3d6-104">Azure AD Connect의 동기화 기능에는 두 가지 구성 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-104">The synchronization feature of Azure AD Connect has two components:</span></span>

* <span data-ttu-id="1c3d6-105">**Azure AD Connect 동기화**라고 하는 온-프레미스 구성 요소(**동기화 엔진**이라고도 함)</span><span class="sxs-lookup"><span data-stu-id="1c3d6-105">The on-premises component named **Azure AD Connect sync**, also called **sync engine**.</span></span>
* <span data-ttu-id="1c3d6-106">**Azure AD Connect 동기화 서비스**</span><span class="sxs-lookup"><span data-stu-id="1c3d6-106">The service residing in Azure AD also known as **Azure AD Connect sync service**</span></span>

<span data-ttu-id="1c3d6-107">이 항목에서는 다음 **Azure AD Connect 동기화 서비스** 기능 작동 방법 및 Windows PowerShell을 사용하여 구성할 수 있는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-107">This topic explains how the following features of the **Azure AD Connect sync service** work and how you can configure them using Windows PowerShell.</span></span>

<span data-ttu-id="1c3d6-108">이러한 설정은 [Windows PowerShell용 Azure Active Directory 모듈](http://aka.ms/aadposh)에서 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-108">These settings are configured by the [Azure Active Directory Module for Windows PowerShell](http://aka.ms/aadposh).</span></span> <span data-ttu-id="1c3d6-109">Azure AD Connect에서 다운로드하여 별도로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-109">Download and install it separately from Azure AD Connect.</span></span> <span data-ttu-id="1c3d6-110">이 항목에서 설명한 cmdlet은 [2016년 3월 릴리스(빌드 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1)에 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-110">The cmdlets documented in this topic were introduced in the [2016 March release (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span></span> <span data-ttu-id="1c3d6-111">이 항목에서 설명하는 cmdlet이 없거나 동일한 결과가 생성되지 않는 경우 최신 버전을 실행하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-111">If you do not have the cmdlets documented in this topic or they do not produce the same result, then make sure you run the latest version.</span></span>

<span data-ttu-id="1c3d6-112">Azure AD 디렉터리의 구성을 보려면 `Get-MsolDirSyncFeatures`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-112">To see the configuration in your Azure AD directory, run `Get-MsolDirSyncFeatures`.</span></span>  
<span data-ttu-id="1c3d6-113">![Get-MsolDirSyncFeatures 결과](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span><span class="sxs-lookup"><span data-stu-id="1c3d6-113">![Get-MsolDirSyncFeatures result](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span></span>

<span data-ttu-id="1c3d6-114">이러한 설정 중 대부분은 Azure AD Connect에서만 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-114">Many of these settings can only be changed by Azure AD Connect.</span></span>

<span data-ttu-id="1c3d6-115">다음 설정은 `Set-MsolDirSyncFeature`에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-115">The following settings can be configured by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="1c3d6-116">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="1c3d6-116">DirSyncFeature</span></span> | <span data-ttu-id="1c3d6-117">주석</span><span class="sxs-lookup"><span data-stu-id="1c3d6-117">Comment</span></span> |
| --- | --- |
| [<span data-ttu-id="1c3d6-118">EnableSoftMatchOnUpn</span><span class="sxs-lookup"><span data-stu-id="1c3d6-118">EnableSoftMatchOnUpn</span></span>](#userprincipalname-soft-match) |<span data-ttu-id="1c3d6-119">개체가 기본 SMTP 주소뿐만 아니라 userPrincipalName에 대해 가입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-119">Allows objects to join on userPrincipalName in addition to primary SMTP address.</span></span> |
| [<span data-ttu-id="1c3d6-120">SynchronizeUpnForManagedUsers</span><span class="sxs-lookup"><span data-stu-id="1c3d6-120">SynchronizeUpnForManagedUsers</span></span>](#synchronize-userprincipalname-updates) |<span data-ttu-id="1c3d6-121">관리되는/허가된(페더레이션되지 않은) 사용자에 대한 userPrincipalName 특성을 동기화 엔진이 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-121">Allows the sync engine to update the userPrincipalName attribute for managed/licensed (non-federated) users.</span></span> |

<span data-ttu-id="1c3d6-122">기능을 사용하도록 설정한 후 다시 해제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-122">After you have enabled a feature, it cannot be disabled again.</span></span>

> [!NOTE]
> <span data-ttu-id="1c3d6-123">2016년 8월 24일에서 *중복 특성 복원력* 기능은 새로운 Azure AD 디렉터리에 대해 기본적으로 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-123">From August 24, 2016 the feature *Duplicate attribute resiliency* is enabled by default for new Azure AD directories.</span></span> <span data-ttu-id="1c3d6-124">또한 이 기능은 이 날짜 이전에 생성된 디렉터리에서 롤아웃되고 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-124">This feature will also be rolled out and enabled on directories created before this date.</span></span> <span data-ttu-id="1c3d6-125">디렉터리가 이 기능을 사용하도록 설정하면 전자 메일 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-125">You will receive an email notification when your directory is about to get this feature enabled.</span></span>
> 
> 

<span data-ttu-id="1c3d6-126">다음 설정은 Azure AD Connect에서 구성되며 `Set-MsolDirSyncFeature`으로 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-126">The following settings are configured by Azure AD Connect and cannot be modified by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="1c3d6-127">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="1c3d6-127">DirSyncFeature</span></span> | <span data-ttu-id="1c3d6-128">주석</span><span class="sxs-lookup"><span data-stu-id="1c3d6-128">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="1c3d6-129">DeviceWriteback</span><span class="sxs-lookup"><span data-stu-id="1c3d6-129">DeviceWriteback</span></span> |[<span data-ttu-id="1c3d6-130">Azure AD Connect: 장치 쓰기 저장 사용</span><span class="sxs-lookup"><span data-stu-id="1c3d6-130">Azure AD Connect: Enabling device writeback</span></span>](active-directory-aadconnect-feature-device-writeback.md) |
| <span data-ttu-id="1c3d6-131">DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="1c3d6-131">DirectoryExtensions</span></span> |[<span data-ttu-id="1c3d6-132">Azure AD Connect 동기화: 디렉터리 확장</span><span class="sxs-lookup"><span data-stu-id="1c3d6-132">Azure AD Connect sync: Directory extensions</span></span>](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [<span data-ttu-id="1c3d6-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span><span class="sxs-lookup"><span data-stu-id="1c3d6-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span></span>](#duplicate-attribute-resiliency) |<span data-ttu-id="1c3d6-134">내보내는 동안 전체 개체가 실패한 것이 아니라 또 다른 개체의 복제본인 경우 특성을 격리시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-134">Allows an attribute to be quarantined when it is a duplicate of another object rather than failing the entire object during export.</span></span> |
| <span data-ttu-id="1c3d6-135">PasswordSync</span><span class="sxs-lookup"><span data-stu-id="1c3d6-135">PasswordSync</span></span> |[<span data-ttu-id="1c3d6-136">Azure AD Connect 동기화로 암호 동기화 구현</span><span class="sxs-lookup"><span data-stu-id="1c3d6-136">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md) |
| <span data-ttu-id="1c3d6-137">UnifiedGroupWriteback</span><span class="sxs-lookup"><span data-stu-id="1c3d6-137">UnifiedGroupWriteback</span></span> |[<span data-ttu-id="1c3d6-138">미리 보기: 그룹 쓰기 저장</span><span class="sxs-lookup"><span data-stu-id="1c3d6-138">Preview: Group writeback</span></span>](active-directory-aadconnect-feature-preview.md#group-writeback) |
| <span data-ttu-id="1c3d6-139">UserWriteback</span><span class="sxs-lookup"><span data-stu-id="1c3d6-139">UserWriteback</span></span> |<span data-ttu-id="1c3d6-140">현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-140">Not currently supported.</span></span> |

## <a name="duplicate-attribute-resiliency"></a><span data-ttu-id="1c3d6-141">중복 특성 복원력</span><span class="sxs-lookup"><span data-stu-id="1c3d6-141">Duplicate attribute resiliency</span></span>
<span data-ttu-id="1c3d6-142">중복된 UPN/proxyAddresses를 가진 개체를 프로비전하는 데 실패하는 대신 중복된 특성은 "격리"되고 임시 값이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-142">Instead of failing to provision objects with duplicate UPNs / proxyAddresses, the duplicated attribute is “quarantined” and a temporary value is assigned.</span></span> <span data-ttu-id="1c3d6-143">충돌이 해결되면 임시 UPN은 적절한 값으로 자동으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-143">When the conflict is resolved, the temporary UPN is changed to the proper value automatically.</span></span> <span data-ttu-id="1c3d6-144">자세한 내용은 [ID 동기화 및 중복 특성 복원력](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-144">For more details, see [Identity synchronization and duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="userprincipalname-soft-match"></a><span data-ttu-id="1c3d6-145">UserPrincipalName 소프트 일치</span><span class="sxs-lookup"><span data-stu-id="1c3d6-145">UserPrincipalName soft match</span></span>
<span data-ttu-id="1c3d6-146">이 기능을 사용하도록 설정하면 [기본 SMTP 주소](https://support.microsoft.com/kb/2641663)외에도 UPN에 소프트 일치를 사용하고 항상 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-146">When this feature is enabled, soft-match is enabled for UPN in addition to the [primary SMTP address](https://support.microsoft.com/kb/2641663), which is always enabled.</span></span> <span data-ttu-id="1c3d6-147">Azure AD의 기존 클라우드 사용자를 온-프레미스 사용자와 일치하는 데 소프트 일치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-147">Soft-match is used to match existing cloud users in Azure AD with on-premises users.</span></span>

<span data-ttu-id="1c3d6-148">온-프레미스 AD 계정이 클라우드에서 만든 기존 계정과 일치해야 하고 Exchange Online을 사용하지 않는 경우 이 기능은 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-148">If you need to match on-premises AD accounts with existing accounts created in the cloud and you are not using Exchange Online, then this feature is useful.</span></span> <span data-ttu-id="1c3d6-149">이 시나리오에서는 일반적으로 클라우드에서 SMTP 특성을 설정할 이유가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-149">In this scenario, you generally don’t have a reason to set the SMTP attribute in the cloud.</span></span>

<span data-ttu-id="1c3d6-150">이 기능은 새로 만든 Azure AD 디렉터리에 기본적으로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-150">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="1c3d6-151">다음을 실행하여 이 기능을 사용하도록 설정했는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-151">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

<span data-ttu-id="1c3d6-152">Azure AD 디렉터리에서 이 기능을 사용하도록 설정하지 않은 경우 다음을 실행하여 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-152">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a><span data-ttu-id="1c3d6-153">UserPrincipalName 업데이트 동기화</span><span class="sxs-lookup"><span data-stu-id="1c3d6-153">Synchronize userPrincipalName updates</span></span>
<span data-ttu-id="1c3d6-154">경험상 다음 조건이 모두 충족되지 않으면 온-프레미스에서 동기화 서비스를 사용하여 UserPrincipalName 특성에 대한 업데이트는 차단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-154">Historically, updates to the UserPrincipalName attribute using the sync service from on-premises has been blocked, unless both of these conditions are true:</span></span>

* <span data-ttu-id="1c3d6-155">사용자가 관리됨(페더레이션되지 않음)</span><span class="sxs-lookup"><span data-stu-id="1c3d6-155">The user is managed (non-federated).</span></span>
* <span data-ttu-id="1c3d6-156">사용자에게 라이선스가 할당되지 않음</span><span class="sxs-lookup"><span data-stu-id="1c3d6-156">The user has not been assigned a license.</span></span>

<span data-ttu-id="1c3d6-157">자세한 내용은 [Office 365, Azure 또는 Intune의 사용자 이름이 온-프레미스 UPN 또는 대체 로그인 ID와 일치하지 않음](https://support.microsoft.com/kb/2523192)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-157">For more details, see [User names in Office 365, Azure, or Intune don't match the on-premises UPN or alternate login ID](https://support.microsoft.com/kb/2523192).</span></span>

<span data-ttu-id="1c3d6-158">이 기능을 사용하도록 설정하면 userPrincipalName이 변경된 온-프레미스이고 암호 동기화를 사용하는 경우 동기화 엔진이 이를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-158">Enabling this feature allows the sync engine to update the userPrincipalName when it is changed on-premises and you use password sync.</span></span> <span data-ttu-id="1c3d6-159">페더레이션을 사용하는 경우 이 기능은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-159">If you use federation, this feature is not supported.</span></span>

<span data-ttu-id="1c3d6-160">이 기능은 새로 만든 Azure AD 디렉터리에 기본적으로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-160">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="1c3d6-161">다음을 실행하여 이 기능을 사용하도록 설정했는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-161">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

<span data-ttu-id="1c3d6-162">Azure AD 디렉터리에서 이 기능을 사용하도록 설정하지 않은 경우 다음을 실행하여 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-162">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

<span data-ttu-id="1c3d6-163">이 기능을 사용하도록 설정하면 기존 userPrincipalName 값이 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-163">After enabling this feature, existing userPrincipalName values will remain as-is.</span></span> <span data-ttu-id="1c3d6-164">userPrincipalName 특성 온-프레미스의 다음 변경 시 사용자에 대한 일반 델타 동기화가 UPN을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3d6-164">On next change of the userPrincipalName attribute on-premises, the normal delta sync on users will update the UPN.</span></span>  

## <a name="see-also"></a><span data-ttu-id="1c3d6-165">참고 항목</span><span class="sxs-lookup"><span data-stu-id="1c3d6-165">See also</span></span>
* [<span data-ttu-id="1c3d6-166">Azure AD Connect 동기화</span><span class="sxs-lookup"><span data-stu-id="1c3d6-166">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="1c3d6-167">[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)</span><span class="sxs-lookup"><span data-stu-id="1c3d6-167">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

