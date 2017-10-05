---
title: "Azure AD Connect 동기화로 암호 동기화 문제 해결 | Microsoft Docs"
description: "이 문서에서는 암호 동기화 문제를 해결하는 방법에 대한 정보를 제공합니다."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 33fa6a8867764975a57b8727e7705529d1d7506a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a><span data-ttu-id="7577a-103">Azure AD Connect 동기화를 사용하여 암호 동기화 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7577a-103">Troubleshoot password synchronization with Azure AD Connect sync</span></span>
<span data-ttu-id="7577a-104">이 항목에서는 암호 동기화 문제를 해결하는 방법에 대한 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-104">This topic provides steps for how to troubleshoot issues with password synchronization.</span></span> <span data-ttu-id="7577a-105">암호가 예상대로 동기화되지 않으면 사용자의 하위 집합 또는 모든 사용자의 암호일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-105">If passwords are not synchronizing as expected, it can be either for a subset of users or for all users.</span></span> <span data-ttu-id="7577a-106">버전 1.1.524.0 이상인 Azure AD(Azure Active Directory) Connect 배포의 경우 이제 암호 동기화 문제를 해결하는 데 사용할 수 있는 진단 cmdlet이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-106">For Azure Active Directory (Azure AD) Connect deployment with version 1.1.524.0 or later, there is now a diagnostic cmdlet that you can use to troubleshoot password synchronization issues:</span></span>

* <span data-ttu-id="7577a-107">암호가 동기화되지 않는 문제가 있으면 [암호가 동기화되지 않음: 진단 cmdlet을 사용하여 문제 해결](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7577a-107">If you have an issue where no passwords are synchronized, refer to the [No passwords are synchronized: troubleshoot by using the diagnostic cmdlet](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

* <span data-ttu-id="7577a-108">개별 개체에 문제가 있으면 [한 개체가 암호를 동기화하지 않음: 진단 cmdlet을 사용하여 문제 해결](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7577a-108">If you have an issue with individual objects, refer to the [One object is not synchronizing passwords: troubleshoot by using the diagnostic cmdlet](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

<span data-ttu-id="7577a-109">이전 버전의 Azure AD Connect 배포:</span><span class="sxs-lookup"><span data-stu-id="7577a-109">For older versions of Azure AD Connect deployment:</span></span>

* <span data-ttu-id="7577a-110">암호가 동기화되지 않는 문제가 있으면 [암호가 동기화되지 않음: 수동 문제 해결 단계](#no-passwords-are-synchronized-manual-troubleshooting-steps) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7577a-110">If you have an issue where no passwords are synchronized, refer to the [No passwords are synchronized: manual troubleshooting steps](#no-passwords-are-synchronized-manual-troubleshooting-steps) section.</span></span>

* <span data-ttu-id="7577a-111">개별 개체에 문제가 있으면 [한 개체가 암호를 동기화하지 않음: 수동 문제 해결 단계](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7577a-111">If you have an issue with individual objects, refer to the [One object is not synchronizing passwords: manual troubleshooting steps](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) section.</span></span>

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet"></a><span data-ttu-id="7577a-112">암호가 동기화되지 않음: 진단 cmdlet을 사용하여 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7577a-112">No passwords are synchronized: troubleshoot by using the diagnostic cmdlet</span></span>
<span data-ttu-id="7577a-113">`Invoke-ADSyncDiagnostics` cmdlet을 사용하여 암호가 동기화되지 않은 이유를 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-113">You can use the `Invoke-ADSyncDiagnostics` cmdlet to figure out why no passwords are synchronized.</span></span>

> [!NOTE]
> <span data-ttu-id="7577a-114">`Invoke-ADSyncDiagnostics` cmdlet은 Azure AD Connect 버전 1.1.524.0 이상에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-114">The `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-the-diagnostics-cmdlet"></a><span data-ttu-id="7577a-115">진단 cmdlet 실행</span><span class="sxs-lookup"><span data-stu-id="7577a-115">Run the diagnostics cmdlet</span></span>
<span data-ttu-id="7577a-116">암호가 동기화되지 않는 문제를 해결하려면</span><span class="sxs-lookup"><span data-stu-id="7577a-116">To troubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="7577a-117">**관리자 권한으로 실행** 옵션을 사용하여 Azure AD Connect 서버에서 새 Windows PowerShell 세션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-117">Open a new Windows PowerShell session on your Azure AD Connect server with the **Run as Administrator** option.</span></span>

2. <span data-ttu-id="7577a-118">`Set-ExecutionPolicy RemoteSigned` 또는 `Set-ExecutionPolicy Unrestricted`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-118">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="7577a-119">`Import-Module ADSyncDiagnostics`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-119">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="7577a-120">`Invoke-ADSyncDiagnostics -PasswordSync`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-120">Run `Invoke-ADSyncDiagnostics -PasswordSync`.</span></span>

### <a name="understand-the-results-of-the-cmdlet"></a><span data-ttu-id="7577a-121">cmdlet의 결과 이해</span><span class="sxs-lookup"><span data-stu-id="7577a-121">Understand the results of the cmdlet</span></span>
<span data-ttu-id="7577a-122">진단 cmdlet은 다음 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-122">The diagnostic cmdlet performs the following checks:</span></span>

* <span data-ttu-id="7577a-123">Azure AD 테넌트에 암호 동기화 기능이 사용되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-123">Validates that the password synchronization feature is enabled for your Azure AD tenant.</span></span>

* <span data-ttu-id="7577a-124">Azure AD Connect 서버가 준비 모드에 있지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-124">Validates that the Azure AD Connect server is not in staging mode.</span></span>

* <span data-ttu-id="7577a-125">각각의 기존 온-프레미스 Active Directory 커넥터(기존 Active Directory 포리스트에 해당)에 대해 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-125">For each existing on-premises Active Directory connector (which corresponds to an existing Active Directory forest):</span></span>

   * <span data-ttu-id="7577a-126">암호 동기화 기능이 사용되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-126">Validates that the password synchronization feature is enabled.</span></span>
   
   * <span data-ttu-id="7577a-127">Windows 응용 프로그램 이벤트 로그에서 암호 동기화 하트비트 이벤트를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-127">Searches for password synchronization heartbeat events in the Windows Application Event logs.</span></span>

   * <span data-ttu-id="7577a-128">온-프레미스 Active Directory 커넥터 아래의 각 Active Directory 도메인에 대해 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-128">For each Active Directory domain under the on-premises Active Directory connector:</span></span>

      * <span data-ttu-id="7577a-129">Azure AD Connect 서버에서 도메인에 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-129">Validates that the domain is reachable from the Azure AD Connect server.</span></span>

      * <span data-ttu-id="7577a-130">온-프레미스 Active Directory 커넥터에서 사용되는 AD DS(Active Directory Domain Services) 계정에 올바른 사용자 이름, 암호 및 암호 동기화에 필요한 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-130">Validates that the Active Directory Domain Services (AD DS) accounts used by the on-premises Active Directory connector has the correct username, password, and permissions required for password synchronization.</span></span>

<span data-ttu-id="7577a-131">다음 다이어그램은 단일 도메인 온-프레미스 Active Directory 토폴로지에 대한 cmdlet의 결과를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-131">The following diagram illustrates the results of the cmdlet for a single-domain, on-premises Active Directory topology:</span></span>

![암호 동기화에 대한 진단 출력](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

<span data-ttu-id="7577a-133">이 섹션의 나머지 부분에서는 cmdlet 및 해당 문제에서 반환되는 특정 결과에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-133">The rest of this section describes specific results that are returned by the cmdlet and corresponding issues.</span></span>

#### <a name="password-synchronization-feature-isnt-enabled"></a><span data-ttu-id="7577a-134">암호 동기화 기능이 사용되지 않음</span><span class="sxs-lookup"><span data-stu-id="7577a-134">Password synchronization feature isn't enabled</span></span>
<span data-ttu-id="7577a-135">Azure AD Connect 마법사를 통해 암호 동기화를 사용하도록 설정하지 않은 경우 다음 오류가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-135">If you haven't enabled password synchronization by using the Azure AD Connect wizard, the following error is returned:</span></span>

![암호 동기화가 사용되지 않음](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a><span data-ttu-id="7577a-137">Azure AD Connect 서버가 준비 모드에 있음</span><span class="sxs-lookup"><span data-stu-id="7577a-137">Azure AD Connect server is in staging mode</span></span>
<span data-ttu-id="7577a-138">Azure AD Connect 서버가 준비 모드에 있으면 암호 동기화가 일시적으로 비활성화되고 다음 오류가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-138">If the Azure AD Connect server is in staging mode, password synchronization is temporarily disabled, and the following error is returned:</span></span>

![Azure AD Connect 서버가 준비 모드에 있음](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a><span data-ttu-id="7577a-140">암호 동기화 하트비트 이벤트 없음</span><span class="sxs-lookup"><span data-stu-id="7577a-140">No password synchronization heartbeat events</span></span>
<span data-ttu-id="7577a-141">각각의 온-프레미스 Active Directory 커넥터에 자체 암호 동기화 채널이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-141">Each on-premises Active Directory connector has its own password synchronization channel.</span></span> <span data-ttu-id="7577a-142">암호 동기화 채널이 설정되었으며 동기화할 암호 변경 내용이 없는 경우 Windows 응용 프로그램 이벤트 로그 아래에 하트비트 이벤트(EventId 654)가 30분마다 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-142">When the password synchronization channel is established and there aren't any password changes to be synchronized, a heartbeat event (EventId 654) is generated once every 30 minutes under the Windows Application Event Log.</span></span> <span data-ttu-id="7577a-143">각각의 온-프레미스 Active Directory 커넥터에 대해 cmdlet은 지난 3시간 동안의 해당 하트비트 이벤트를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-143">For each on-premises Active Directory connector, the cmdlet searches for corresponding heartbeat events in the past three hours.</span></span> <span data-ttu-id="7577a-144">하트비트 이벤트가 발견되면 다음 오류가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-144">If no heartbeat event is found, the following error is returned:</span></span>

![암호 동기화 하트비트 이벤트 없음](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a><span data-ttu-id="7577a-146">AD DS 계정에 올바른 사용 권한이 없음</span><span class="sxs-lookup"><span data-stu-id="7577a-146">AD DS account does not have correct permissions</span></span>
<span data-ttu-id="7577a-147">온-프레미스 Active Directory 커넥터가 암호 해시 동기화에 사용하는 AD DS 계정에 적절한 사용 권한이 없으면 다음 오류가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-147">If the AD DS account that's used by the on-premises Active Directory connector to synchronize password hashes does not have the appropriate permissions, the following error is returned:</span></span>

![잘못된 자격 증명](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a><span data-ttu-id="7577a-149">잘못된 AD DS 계정 사용자 이름 또는 암호</span><span class="sxs-lookup"><span data-stu-id="7577a-149">Incorrect AD DS account username or password</span></span>
<span data-ttu-id="7577a-150">온-프레미스 Active Directory 커넥터가 암호 해시 동기화에 사용하는 AD DS 계정에 잘못된 사용자 이름 또는 암호가 있으면 다음 오류가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-150">If the AD DS account used by the on-premises Active Directory connector to synchronize password hashes has an incorrect username or password, the following error is returned:</span></span>

![잘못된 자격 증명](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet"></a><span data-ttu-id="7577a-152">한 개체가 암호를 동기화하지 않음: 진단 cmdlet을 사용하여 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7577a-152">One object is not synchronizing passwords: troubleshoot by using the diagnostic cmdlet</span></span>
<span data-ttu-id="7577a-153">`Invoke-ADSyncDiagnostics` cmdlet을 사용하여 한 개체가 암호를 동기화하지 않는 이유를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-153">You can use the `Invoke-ADSyncDiagnostics` cmdlet to determine why one object is not synchronizing passwords.</span></span>

> [!NOTE]
> <span data-ttu-id="7577a-154">`Invoke-ADSyncDiagnostics` cmdlet은 Azure AD Connect 버전 1.1.524.0 이상에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-154">The `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-the-diagnostics-cmdlet"></a><span data-ttu-id="7577a-155">진단 cmdlet 실행</span><span class="sxs-lookup"><span data-stu-id="7577a-155">Run the diagnostics cmdlet</span></span>
<span data-ttu-id="7577a-156">암호가 동기화되지 않는 문제를 해결하려면</span><span class="sxs-lookup"><span data-stu-id="7577a-156">To troubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="7577a-157">**관리자 권한으로 실행** 옵션을 사용하여 Azure AD Connect 서버에서 새 Windows PowerShell 세션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-157">Open a new Windows PowerShell session on your Azure AD Connect server with the **Run as Administrator** option.</span></span>

2. <span data-ttu-id="7577a-158">`Set-ExecutionPolicy RemoteSigned` 또는 `Set-ExecutionPolicy Unrestricted`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-158">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="7577a-159">`Import-Module ADSyncDiagnostics`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-159">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="7577a-160">다음 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-160">Run the following cmdlet:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   <span data-ttu-id="7577a-161">예:</span><span class="sxs-lookup"><span data-stu-id="7577a-161">For example:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-the-results-of-the-cmdlet"></a><span data-ttu-id="7577a-162">cmdlet의 결과 이해</span><span class="sxs-lookup"><span data-stu-id="7577a-162">Understand the results of the cmdlet</span></span>
<span data-ttu-id="7577a-163">진단 cmdlet은 다음 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-163">The diagnostic cmdlet performs the following checks:</span></span>

* <span data-ttu-id="7577a-164">Active Directory 커넥터 공간, 메타버스 및 Azure AD 커넥터 공간에서 Active Directory 개체의 상태를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-164">Examines the state of the Active Directory object in the Active Directory connector space, Metaverse, and Azure AD connector space.</span></span>

* <span data-ttu-id="7577a-165">암호 동기화가 사용되고 Active Directory 개체에 적용되는 동기화 규칙이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-165">Validates that there are synchronization rules with password synchronization enabled and applied to the Active Directory object.</span></span>

* <span data-ttu-id="7577a-166">개체의 암호를 동기화하려는 마지막 시도의 결과를 검색하고 표시하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-166">Attempts to retrieve and display the results of the last attempt to synchronize the password for the object.</span></span>

<span data-ttu-id="7577a-167">다음 다이어그램은 단일 개체에 대한 암호 동기화 문제를 해결하는 경우의 cmdlet 결과를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-167">The following diagram illustrates the results of the cmdlet when troubleshooting password synchronization for a single object:</span></span>

![암호 동기화에 대한 진단 출력 - 단일 개체](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

<span data-ttu-id="7577a-169">이 섹션의 나머지 부분에서는 cmdlet 및 해당 문제에서 반환되는 특정 결과에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-169">The rest of this section describes specific results returned by the cmdlet and corresponding issues.</span></span>

#### <a name="the-active-directory-object-isnt-exported-to-azure-ad"></a><span data-ttu-id="7577a-170">Active Directory 개체가 Azure AD로 내보내지지 않음</span><span class="sxs-lookup"><span data-stu-id="7577a-170">The Active Directory object isn't exported to Azure AD</span></span>
<span data-ttu-id="7577a-171">이 온-프레미스 Active Directory 계정에 대한 암호 동기화는 Azure AD 테넌트에 해당 개체가 없으므로 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-171">Password synchronization for this on-premises Active Directory account fails because there is no corresponding object in the Azure AD tenant.</span></span> <span data-ttu-id="7577a-172">다음 오류가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-172">The following error is returned:</span></span>

![Azure AD 개체가 없음](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a><span data-ttu-id="7577a-174">사용자에게 임시 암호가 있음</span><span class="sxs-lookup"><span data-stu-id="7577a-174">User has a temporary password</span></span>
<span data-ttu-id="7577a-175">현재, Azure AD Connect는 임시 암호를 Azure AD와 동기화하는 기능을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-175">Currently, Azure AD Connect does not support synchronizing temporary passwords with Azure AD.</span></span> <span data-ttu-id="7577a-176">**다음 로그온할 때 암호 변경** 옵션이 온-프레미스 Active Directory 사용자에 설정되어 있으면 임시 암호로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-176">A password is considered to be temporary if the **Change password at next logon** option is set on the on-premises Active Directory user.</span></span> <span data-ttu-id="7577a-177">다음 오류가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-177">The following error is returned:</span></span>

![임시 암호는 내보내지지 않음](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-to-synchronize-password-arent-available"></a><span data-ttu-id="7577a-179">마지막 암호 동기화 시도의 결과를 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="7577a-179">Results of last attempt to synchronize password aren't available</span></span>
<span data-ttu-id="7577a-180">기본적으로 Azure AD Connect는 7일 동안의 암호 동기화 시도 결과를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-180">By default, Azure AD Connect stores the results of password synchronization attempts for seven days.</span></span> <span data-ttu-id="7577a-181">선택한 Active Directory 개체에 대한 결과를 사용할 수 없는 경우 다음 경고가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-181">If there are no results available for the selected Active Directory object, the following warning is returned:</span></span>

![단일 개체에 대한 진단 출력 - 암호 동기화 기록 없음](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a><span data-ttu-id="7577a-183">암호가 동기화되지 않음: 수동 문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="7577a-183">No passwords are synchronized: manual troubleshooting steps</span></span>
<span data-ttu-id="7577a-184">암호가 동기화되지 않는 이유를 확인하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="7577a-184">Follow these steps to determine why no passwords are synchronized:</span></span>

1. <span data-ttu-id="7577a-185">연결 서버가 [스테이징 모드](active-directory-aadconnectsync-operations.md#staging-mode)인가요?</span><span class="sxs-lookup"><span data-stu-id="7577a-185">Is the Connect server in [staging mode](active-directory-aadconnectsync-operations.md#staging-mode)?</span></span> <span data-ttu-id="7577a-186">스테이징 모드의 서버는 암호를 동기화하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-186">A server in staging mode does not synchronize any passwords.</span></span>

2. <span data-ttu-id="7577a-187">[암호 동기화 설정 상태 가져오기](#get-the-status-of-password-sync-settings) 섹션에서 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-187">Run the script in the [Get the status of password sync settings](#get-the-status-of-password-sync-settings) section.</span></span> <span data-ttu-id="7577a-188">암호 동기화 구성의 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-188">It gives you an overview of the password sync configuration.</span></span>  

    ![암호 동기화 설정의 PowerShell 스크립트 출력](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. <span data-ttu-id="7577a-190">Azure AD에서 이 기능이 사용되지 않거나 동기화 채널 상태가 사용되지 않는 경우 Connect 설치 마법사를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-190">If the feature is not enabled in Azure AD or if the sync channel status is not enabled, run the Connect installation wizard.</span></span> <span data-ttu-id="7577a-191">**동기화 옵션 사용자 지정**을 선택하고 암호 동기화의 선택을 취소합니다. 이 변경 내용은 기능을 일시적으로 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-191">Select **Customize synchronization options**, and unselect password sync. This change temporarily disables the feature.</span></span> <span data-ttu-id="7577a-192">그런 다음 마법사를 다시 실행하고 암호 동기화를 다시 사용합니다. 스크립트를 다시 실행하여 구성이 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-192">Then run the wizard again and re-enable password sync. Run the script again to verify that the configuration is correct.</span></span>

4. <span data-ttu-id="7577a-193">이벤트 로그에서 오류를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-193">Look in the event log for errors.</span></span> <span data-ttu-id="7577a-194">문제를 나타내는 다음 이벤트를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-194">Look for the following events, which would indicate a problem:</span></span>
    * <span data-ttu-id="7577a-195">원본: "디렉터리 동기화" ID: 0, 611, 652, 655 이러한 이벤트가 표시되면 연결 문제가 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-195">Source: "Directory synchronization" ID: 0, 611, 652, 655 If you see these events, you have a connectivity problem.</span></span> <span data-ttu-id="7577a-196">이벤트 로그 메시지에는 문제가 있는 포리스트 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-196">The event log message contains forest information where you have a problem.</span></span> <span data-ttu-id="7577a-197">자세한 내용은 [연결 문제](#connectivity problem)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7577a-197">For more information, see [Connectivity problem](#connectivity problem).</span></span>

5. <span data-ttu-id="7577a-198">하트비트가 표시되지 않거나 아무 작동도 진행되지 않으면 [모든 암호의 전체 동기화 트리거](#trigger-a-full-sync-of-all-passwords)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-198">If you see no heartbeat or if nothing else worked, run [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span> <span data-ttu-id="7577a-199">스크립트를 한 번만 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-199">Run the script only once.</span></span>

6. <span data-ttu-id="7577a-200">[암호를 동기화하지 않는 한 개체의 문제 해결](#one-object-is-not-synchronizing-passwords) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7577a-200">See the [Troubleshoot one object that is not synchronizing passwords](#one-object-is-not-synchronizing-passwords) section.</span></span>

### <a name="connectivity-problems"></a><span data-ttu-id="7577a-201">연결 문제</span><span class="sxs-lookup"><span data-stu-id="7577a-201">Connectivity problems</span></span>

<span data-ttu-id="7577a-202">Azure AD와 연결되어 있나요?</span><span class="sxs-lookup"><span data-stu-id="7577a-202">Do you have connectivity with Azure AD?</span></span>

<span data-ttu-id="7577a-203">계정에 모든 도메인에서 암호 해시를 읽는 데 필요한 권한이 있나요?</span><span class="sxs-lookup"><span data-stu-id="7577a-203">Does the account have required permissions to read the password hashes in all domains?</span></span> <span data-ttu-id="7577a-204">기본 설정을 사용하여 Connect를 설치한 경우 사용 권한은 이미 올바른 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-204">If you installed Connect by using Express settings, the permissions should already be correct.</span></span> 

<span data-ttu-id="7577a-205">사용자 지정 설치를 사용한 경우 다음을 수행하여 사용 권한을 수동으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-205">If you used custom installation, set the permissions manually by doing the following:</span></span>
    
1. <span data-ttu-id="7577a-206">Active Directory Connector에서 사용되는 계정을 찾으려면 **Synchronization Service Manager**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-206">To find the account used by the Active Directory connector, start **Synchronization Service Manager**.</span></span> 
 
2. <span data-ttu-id="7577a-207">**커넥터**로 이동한 다음 문제를 해결하려는 온-프레미스 Active Directory 포리스트를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-207">Go to **Connectors**, and then search for the on-premises Active Directory forest you are troubleshooting.</span></span> 
 
3. <span data-ttu-id="7577a-208">커넥터를 선택하고 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-208">Select the connector, and then click **Properties**.</span></span> 
 
4. <span data-ttu-id="7577a-209">**Active Directory 포리스트에 연결**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-209">Go to **Connect to Active Directory Forest**.</span></span>  
    
    ![Active Directory 커넥터에서 사용되는 계정](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    <span data-ttu-id="7577a-211">계정이 있는 사용자 이름 및 도메인을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-211">Note the username and the domain where the account is located.</span></span>
    
5. <span data-ttu-id="7577a-212">**Active Directory 사용자 및 컴퓨터**를 시작한 다음 앞에서 찾은 계정에 대해 포리스트에 있는 모든 도메인의 루트에서 다음 사용 권한이 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-212">Start **Active Directory Users and Computers**, and then verify that the account you found earlier has the follow permissions set at the root of all domains in your forest:</span></span>
    * <span data-ttu-id="7577a-213">디렉터리 변경 내용 복제</span><span class="sxs-lookup"><span data-stu-id="7577a-213">Replicate Directory Changes</span></span>
    * <span data-ttu-id="7577a-214">모든 디렉터리 변경 내용 복제</span><span class="sxs-lookup"><span data-stu-id="7577a-214">Replicate Directory Changes All</span></span>

6. <span data-ttu-id="7577a-215">Azure AD Connect에서 도메인 컨트롤러에 연결할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7577a-215">Are the domain controllers reachable by Azure AD Connect?</span></span> <span data-ttu-id="7577a-216">Connect 서버에서 일부 도메인 컨트롤러에 연결할 수 없는 경우 **기본 설정 도메인 컨트롤러만 사용**을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-216">If the Connect server cannot connect to all domain controllers, configure **Only use preferred domain controller**.</span></span>  
    
    ![Active Directory 커넥터에서 사용되는 도메인 컨트롤러](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. <span data-ttu-id="7577a-218">**Synchronization Service Manager** 및 **디렉터리 파티션 구성**으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-218">Go back to **Synchronization Service Manager** and **Configure Directory Partition**.</span></span> 
 
8. <span data-ttu-id="7577a-219">**디렉터리 파티션 선택**에서 도메인을 선택하고 **기본 설정 도메인 컨트롤러만 사용** 확인란을 선택한 다음 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-219">Select your domain in **Select directory partitions**, select the **Only use preferred domain controllers** check box, and then click **Configure**.</span></span> 

9. <span data-ttu-id="7577a-220">목록에서 Connect가 암호 동기화에 사용해야 하는 도메인 컨트롤러를 입력합니다. 동일한 목록이 가져오기 및 내보내기에도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-220">In the list, enter the domain controllers that Connect should use for password sync. The same list is used for import and export as well.</span></span> <span data-ttu-id="7577a-221">모든 도메인에 대해 이 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-221">Do these steps for all your domains.</span></span>

10. <span data-ttu-id="7577a-222">스크립트에서 하트비트가 없음을 보여 주는 경우 [모든 암호의 전체 동기화 트리거](#trigger-a-full-sync-of-all-passwords)에서 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-222">If the script shows that there is no heartbeat, run the script in [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span>

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a><span data-ttu-id="7577a-223">한 개체가 암호를 동기화하지 않음: 수동 문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="7577a-223">One object is not synchronizing passwords: manual troubleshooting steps</span></span>
<span data-ttu-id="7577a-224">개체의 상태를 검토하여 암호 동기화 문제를 쉽게 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-224">You can easily troubleshoot password synchronization issues by reviewing the status of an object.</span></span>

1. <span data-ttu-id="7577a-225">**Active Directory 사용자 및 컴퓨터**에서 해당 사용자를 검색하고 **다음 로그온할 때 반드시 암호 변경** 확인란이 선택 취소되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-225">In **Active Directory Users and Computers**, search for the user, and then verify that the **User must change password at next logon** check box is cleared.</span></span>  

    ![Active Directory 생산성 높은 암호](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    <span data-ttu-id="7577a-227">확인란이 선택된 경우 사용자에게 로그인하여 암호를 변경하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-227">If the check box is selected, ask the user to sign in and change the password.</span></span> <span data-ttu-id="7577a-228">임시 암호는 Azure AD와 동기화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-228">Temporary passwords are not synchronized with Azure AD.</span></span>

2. <span data-ttu-id="7577a-229">Active Directory에서 암호가 올바른 것 같으면 동기화 엔진에서 사용자를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-229">If the password looks correct in Active Directory, follow the user in the sync engine.</span></span> <span data-ttu-id="7577a-230">온-프레미스 Active Directory에서 Azure AD까지 사용자를 따라 개체에 설명이 포함된 오류가 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-230">By following the user from on-premises Active Directory to Azure AD, you can see whether there is a descriptive error on the object.</span></span>

    <span data-ttu-id="7577a-231">a.</span><span class="sxs-lookup"><span data-stu-id="7577a-231">a.</span></span> <span data-ttu-id="7577a-232">[Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-232">Start the [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span></span>

    <span data-ttu-id="7577a-233">b.</span><span class="sxs-lookup"><span data-stu-id="7577a-233">b.</span></span> <span data-ttu-id="7577a-234">**커넥터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-234">Click **Connectors**.</span></span>

    <span data-ttu-id="7577a-235">c.</span><span class="sxs-lookup"><span data-stu-id="7577a-235">c.</span></span> <span data-ttu-id="7577a-236">사용자가 있는 **Active Directory Connector**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-236">Select the **Active Directory Connector** where the user is located.</span></span>

    <span data-ttu-id="7577a-237">d.</span><span class="sxs-lookup"><span data-stu-id="7577a-237">d.</span></span> <span data-ttu-id="7577a-238">**커넥터 공간 검색**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-238">Select **Search Connector Space**.</span></span>

    <span data-ttu-id="7577a-239">e.</span><span class="sxs-lookup"><span data-stu-id="7577a-239">e.</span></span> <span data-ttu-id="7577a-240">**범위** 상자에서 **DN 또는 앵커**를 선택한 다음 문제를 해결하려는 사용자의 전체 DN을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-240">In the **Scope** box, select **DN or Anchor**, and then enter the full DN of the user you are troubleshooting.</span></span>

    ![DN을 사용하여 커넥터 공간에서 사용자 검색](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    <span data-ttu-id="7577a-242">f.</span><span class="sxs-lookup"><span data-stu-id="7577a-242">f.</span></span> <span data-ttu-id="7577a-243">원하는 사용자를 찾은 후 **속성**을 클릭하여 모든 특성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-243">Locate the user you are looking for, and then click **Properties** to see all the attributes.</span></span> <span data-ttu-id="7577a-244">해당 사용자가 검색 결과에 없으면 [필터링 규칙](active-directory-aadconnectsync-configure-filtering.md)을 확인하고 [변경 내용 적용 및 확인](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes)을 실행하여 사용자가 Connect에 표시되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-244">If the user is not in the search result, verify your [filtering rules](active-directory-aadconnectsync-configure-filtering.md) and make sure that you run [Apply and verify changes](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) for the user to appear in Connect.</span></span>

    <span data-ttu-id="7577a-245">g.</span><span class="sxs-lookup"><span data-stu-id="7577a-245">g.</span></span> <span data-ttu-id="7577a-246">지난주에 대한 개체의 암호 동기화 정보를 보려면 **로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-246">To see the password sync details of the object for the past week, click **Log**.</span></span>  

    ![개체 로그 정보](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    <span data-ttu-id="7577a-248">개체 로그가 비어 있으면 Azure AD Connect가 Active Directory에서 암호 해시를 읽지 못한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-248">If the object log is empty, Azure AD Connect has been unable to read the password hash from Active Directory.</span></span> <span data-ttu-id="7577a-249">[연결 오류](#connectivity-errors) 문제를 계속 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-249">Continue your troubleshooting with [Connectivity Errors](#connectivity-errors).</span></span> <span data-ttu-id="7577a-250">**success** 이외의 값이 표시되면 [암호 동기화 로그](#password-sync-log)의 테이블을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7577a-250">If you see any other value than **success**, refer to the table in [Password sync log](#password-sync-log).</span></span>

    <span data-ttu-id="7577a-251">h.</span><span class="sxs-lookup"><span data-stu-id="7577a-251">h.</span></span> <span data-ttu-id="7577a-252">**계보** 탭을 선택한 다음 **PasswordSync** 열에서 하나 이상의 동기화 규칙이 **True**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-252">Select the **lineage** tab, and make sure that at least one sync rule in the **PasswordSync** column is **True**.</span></span> <span data-ttu-id="7577a-253">기본 구성에서 동기화 규칙의 이름은 **AD에서 들어오기 - User AccountEnabled**입니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-253">In the default configuration, the name of the sync rule is **In from AD - User AccountEnabled**.</span></span>  

    ![사용자에 대한 계보 정보](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    <span data-ttu-id="7577a-255">i.</span><span class="sxs-lookup"><span data-stu-id="7577a-255">i.</span></span> <span data-ttu-id="7577a-256">**메타버스 개체 속성**을 클릭하여 사용자 특성 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-256">Click **Metaverse Object Properties** to display a list of user attributes.</span></span>  

    ![메타버스 정보](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    <span data-ttu-id="7577a-258">**cloudFiltered** 특성이 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-258">Verify that there is no **cloudFiltered** attribute present.</span></span> <span data-ttu-id="7577a-259">도메인 특성(domainFQDN 및 domainNetBios)이 예상 값을 갖는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-259">Make sure that the domain attributes (domainFQDN and domainNetBios) have the expected values.</span></span>

    <span data-ttu-id="7577a-260">j.</span><span class="sxs-lookup"><span data-stu-id="7577a-260">j.</span></span> <span data-ttu-id="7577a-261">**커넥터** 탭을 클릭합니다. 온-프레미스 Active Directory 및 Azure AD 둘 다에 대한 커넥터가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-261">Click the **Connectors** tab. Make sure that you see connectors to both on-premises Active Directory and Azure AD.</span></span>

    ![메타버스 정보](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    <span data-ttu-id="7577a-263">k.</span><span class="sxs-lookup"><span data-stu-id="7577a-263">k.</span></span> <span data-ttu-id="7577a-264">Azure AD를 나타내는 행을 선택하고 **속성**을 클릭한 다음 **계보** 탭을 클릭합니다. 커넥터 공간 개체에 대한 **PasswordSync** 열의 아웃바운드 규칙이 **True**로 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-264">Select the row that represents Azure AD, click **Properties**, and then click the **Lineage** tab. The connector space object should have an outbound rule in the **PasswordSync** column set to **True**.</span></span> <span data-ttu-id="7577a-265">기본 구성에서 동기화 규칙의 이름은 **AAD로 나가기 - 사용자 조인**입니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-265">In the default configuration, the name of the sync rule is **Out to AAD - User Join**.</span></span>  

    ![커넥터 공간 개체 속성 대화 상자](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a><span data-ttu-id="7577a-267">암호 동기화 로그</span><span class="sxs-lookup"><span data-stu-id="7577a-267">Password sync log</span></span>
<span data-ttu-id="7577a-268">상태 열에는 다음과 같은 값을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-268">The status column can have the following values:</span></span>

| <span data-ttu-id="7577a-269">가동 상태</span><span class="sxs-lookup"><span data-stu-id="7577a-269">Status</span></span> | <span data-ttu-id="7577a-270">설명</span><span class="sxs-lookup"><span data-stu-id="7577a-270">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7577a-271">성공</span><span class="sxs-lookup"><span data-stu-id="7577a-271">Success</span></span> |<span data-ttu-id="7577a-272">암호가 성공적으로 동기화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-272">Password has been successfully synchronized.</span></span> |
| <span data-ttu-id="7577a-273">FilteredByTarget</span><span class="sxs-lookup"><span data-stu-id="7577a-273">FilteredByTarget</span></span> |<span data-ttu-id="7577a-274">**다음 로그인할 때 반드시 암호 변경**으로 암호가 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-274">Password is set to **User must change password at next logon**.</span></span> <span data-ttu-id="7577a-275">암호가 동기화되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-275">Password has not been synchronized.</span></span> |
| <span data-ttu-id="7577a-276">NoTargetConnection</span><span class="sxs-lookup"><span data-stu-id="7577a-276">NoTargetConnection</span></span> |<span data-ttu-id="7577a-277">메타버스에 또는 Azure AD 커넥터 공간에 개체가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-277">No object in the metaverse or in the Azure AD connector space.</span></span> |
| <span data-ttu-id="7577a-278">SourceConnectorNotPresent</span><span class="sxs-lookup"><span data-stu-id="7577a-278">SourceConnectorNotPresent</span></span> |<span data-ttu-id="7577a-279">개체를 온-프레미스 Active Directory Connector 공간에서 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-279">No object found in the on-premises Active Directory connector space.</span></span> |
| <span data-ttu-id="7577a-280">TargetNotExportedToDirectory</span><span class="sxs-lookup"><span data-stu-id="7577a-280">TargetNotExportedToDirectory</span></span> |<span data-ttu-id="7577a-281">Azure AD 커넥터 공간에 있는 개체가 아직 내보내지지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-281">The object in the Azure AD connector space has not yet been exported.</span></span> |
| <span data-ttu-id="7577a-282">MigratedCheckDetailsForMoreInfo</span><span class="sxs-lookup"><span data-stu-id="7577a-282">MigratedCheckDetailsForMoreInfo</span></span> |<span data-ttu-id="7577a-283">로그 항목 1.0.9125.0 빌드 전에 만들어졌으며 레거시 상태로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-283">Log entry was created before build 1.0.9125.0 and is shown in its legacy state.</span></span> |
| <span data-ttu-id="7577a-284">오류</span><span class="sxs-lookup"><span data-stu-id="7577a-284">Error</span></span> |<span data-ttu-id="7577a-285">서비스에 알 수 없는 오류가 반환되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-285">Service returned an unknown error.</span></span> |
| <span data-ttu-id="7577a-286">알 수 없음</span><span class="sxs-lookup"><span data-stu-id="7577a-286">Unknown</span></span> |<span data-ttu-id="7577a-287">암호 해시의 배치를 처리하는 동안 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-287">An error occurred while trying to process a batch of password hashes.</span></span>  |
| <span data-ttu-id="7577a-288">MissingAttribute</span><span class="sxs-lookup"><span data-stu-id="7577a-288">MissingAttribute</span></span> |<span data-ttu-id="7577a-289">Azure AD Domain Services에 필요한 특정 특성(예: Kerberos 해시)을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-289">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services are not available.</span></span> |
| <span data-ttu-id="7577a-290">RetryRequestedByTarget</span><span class="sxs-lookup"><span data-stu-id="7577a-290">RetryRequestedByTarget</span></span> |<span data-ttu-id="7577a-291">Azure AD Domain Services에 필요한 특정 특성(예: Kerberos 해시)을 이전에 사용할 수 없었습니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-291">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services were not available previously.</span></span> <span data-ttu-id="7577a-292">사용자의 암호 해시를 다시 동기화하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-292">An attempt to resynchronize the user's password hash is made.</span></span> |

## <a name="scripts-to-help-troubleshooting"></a><span data-ttu-id="7577a-293">문제 해결에 도움이 되는 스크립트</span><span class="sxs-lookup"><span data-stu-id="7577a-293">Scripts to help troubleshooting</span></span>

### <a name="get-the-status-of-password-sync-settings"></a><span data-ttu-id="7577a-294">암호 동기화 설정의 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="7577a-294">Get the status of password sync settings</span></span>
```
Import-Module ADSync
$connectors = Get-ADSyncConnector
$aadConnectors = $connectors | Where-Object {$_.SubType -eq "Windows Azure Active Directory (Microsoft)"}
$adConnectors = $connectors | Where-Object {$_.ConnectorTypeName -eq "AD"}
if ($aadConnectors -ne $null -and $adConnectors -ne $null)
{
    if ($aadConnectors.Count -eq 1)
    {
        $features = Get-ADSyncAADCompanyFeature -ConnectorName $aadConnectors[0].Name
        Write-Host
        Write-Host "Password sync feature enabled in your Azure AD directory: "  $features.PasswordHashSync
        foreach ($adConnector in $adConnectors)
        {
            Write-Host
            Write-Host "Password sync channel status BEGIN ------------------------------------------------------- "
            Write-Host
            Get-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector.Name
            Write-Host
            $pingEvents =
                Get-EventLog -LogName "Application" -Source "Directory Synchronization" -InstanceId 654  -After (Get-Date).AddHours(-3) |
                    Where-Object { $_.Message.ToUpperInvariant().Contains($adConnector.Identifier.ToString("D").ToUpperInvariant()) } |
                    Sort-Object { $_.Time } -Descending
            if ($pingEvents -ne $null)
            {
                Write-Host "Latest heart beat event (within last 3 hours). Time " $pingEvents[0].TimeWritten
            }
            else
            {
                Write-Warning "No ping event found within last 3 hours."
            }
            Write-Host
            Write-Host "Password sync channel status END ------------------------------------------------------- "
            Write-Host
        }
    }
    else
    {
        Write-Warning "More than one Azure AD Connectors found. Please update the script to use the appropriate Connector."
    }
}
Write-Host
if ($aadConnectors -eq $null)
{
    Write-Warning "No Azure AD Connector was found."
}
if ($adConnectors -eq $null)
{
    Write-Warning "No AD DS Connector was found."
}
Write-Host
```

#### <a name="trigger-a-full-sync-of-all-passwords"></a><span data-ttu-id="7577a-295">모든 암호의 전체 동기화 트리거</span><span class="sxs-lookup"><span data-stu-id="7577a-295">Trigger a full sync of all passwords</span></span>
> [!NOTE]
> <span data-ttu-id="7577a-296">이 스크립트는 한 번만 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-296">Run this script only once.</span></span> <span data-ttu-id="7577a-297">이 스크립트를 두 번 이상 실행해야 한다면 문제가 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-297">If you need to run it more than once, something else is the problem.</span></span> <span data-ttu-id="7577a-298">문제를 해결하려면 Microsoft 지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="7577a-298">To troubleshoot the problem, contact Microsoft support.</span></span>

<span data-ttu-id="7577a-299">다음 스크립트를 사용하여 모든 암호의 전체 동기화를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7577a-299">You can trigger a full sync of all passwords by using the following script:</span></span>

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"
$aadConnector = "<CASE SENSITIVE AAD CONNECTOR NAME>"
Import-Module adsync
$c = Get-ADSyncConnector -Name $adConnector
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1
$c.GlobalParameters.Remove($p.Name)
$c.GlobalParameters.Add($p)
$c = Add-ADSyncConnector -Connector $c
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $false
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $true
```

## <a name="next-steps"></a><span data-ttu-id="7577a-300">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7577a-300">Next steps</span></span>
* [<span data-ttu-id="7577a-301">Azure AD Connect 동기화로 암호 동기화 구현</span><span class="sxs-lookup"><span data-stu-id="7577a-301">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md)
* [<span data-ttu-id="7577a-302">Azure AD Connect 동기화: 동기화 옵션 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="7577a-302">Azure AD Connect Sync: Customizing synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="7577a-303">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="7577a-303">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
