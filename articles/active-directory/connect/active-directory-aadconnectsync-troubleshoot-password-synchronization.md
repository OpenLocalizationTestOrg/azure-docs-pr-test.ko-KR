---
title: "Azure AD Connect 동기화로 암호 동기화 aaaTroubleshoot | Microsoft Docs"
description: "이 문서는 방법에 대 한 정보를 제공 tootroubleshoot 암호 동기화 문제."
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
ms.openlocfilehash: 390eafec792cb39251627c14cb754f8bb30035b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a><span data-ttu-id="04787-103">Azure AD Connect 동기화를 사용하여 암호 동기화 문제 해결</span><span class="sxs-lookup"><span data-stu-id="04787-103">Troubleshoot password synchronization with Azure AD Connect sync</span></span>
<span data-ttu-id="04787-104">이 항목에서는 암호 동기화와 함께 tootroubleshoot 발급 하는 방법에 대 한 단계를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-104">This topic provides steps for how tootroubleshoot issues with password synchronization.</span></span> <span data-ttu-id="04787-105">암호가 예상대로 동기화되지 않으면 사용자의 하위 집합 또는 모든 사용자의 암호일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-105">If passwords are not synchronizing as expected, it can be either for a subset of users or for all users.</span></span> <span data-ttu-id="04787-106">Azure Active Directory (Azure AD)에 대 한 배포 1.1.524.0 버전과 연결 또는 이상 버전에서는 이제 진단 cmdlet이 tootroubleshoot 암호 동기화 문제를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-106">For Azure Active Directory (Azure AD) Connect deployment with version 1.1.524.0 or later, there is now a diagnostic cmdlet that you can use tootroubleshoot password synchronization issues:</span></span>

* <span data-ttu-id="04787-107">암호가 동기화는 문제가 있는, 하는 경우 참조 toohello [암호가 동기화: hello 진단 cmdlet을 사용 하 여 문제를 해결](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) 섹션.</span><span class="sxs-lookup"><span data-stu-id="04787-107">If you have an issue where no passwords are synchronized, refer toohello [No passwords are synchronized: troubleshoot by using hello diagnostic cmdlet](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

* <span data-ttu-id="04787-108">개별 개체에 문제가 있는 경우 참조 toohello [하나의 개체만 암호 동기화 되지 않는: hello 진단 cmdlet을 사용 하 여 문제를 해결](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) 섹션.</span><span class="sxs-lookup"><span data-stu-id="04787-108">If you have an issue with individual objects, refer toohello [One object is not synchronizing passwords: troubleshoot by using hello diagnostic cmdlet](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

<span data-ttu-id="04787-109">이전 버전의 Azure AD Connect 배포:</span><span class="sxs-lookup"><span data-stu-id="04787-109">For older versions of Azure AD Connect deployment:</span></span>

* <span data-ttu-id="04787-110">암호가 동기화는 문제가 있는, 하는 경우 참조 toohello [암호가 동기화: 문제 해결 단계는 수동](#no-passwords-are-synchronized-manual-troubleshooting-steps) 섹션.</span><span class="sxs-lookup"><span data-stu-id="04787-110">If you have an issue where no passwords are synchronized, refer toohello [No passwords are synchronized: manual troubleshooting steps](#no-passwords-are-synchronized-manual-troubleshooting-steps) section.</span></span>

* <span data-ttu-id="04787-111">개별 개체에 문제가 있는 경우 참조 toohello [하나의 개체만 암호 동기화 되지 않는: 문제 해결 단계는 수동](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) 섹션.</span><span class="sxs-lookup"><span data-stu-id="04787-111">If you have an issue with individual objects, refer toohello [One object is not synchronizing passwords: manual troubleshooting steps](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) section.</span></span>

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-hello-diagnostic-cmdlet"></a><span data-ttu-id="04787-112">암호가 동기화: hello 진단 cmdlet을 사용 하 여 문제 해결</span><span class="sxs-lookup"><span data-stu-id="04787-112">No passwords are synchronized: troubleshoot by using hello diagnostic cmdlet</span></span>
<span data-ttu-id="04787-113">Hello를 사용할 수 있습니다 `Invoke-ADSyncDiagnostics` cmdlet toofigure 아웃 이유 암호가 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04787-113">You can use hello `Invoke-ADSyncDiagnostics` cmdlet toofigure out why no passwords are synchronized.</span></span>

> [!NOTE]
> <span data-ttu-id="04787-114">hello `Invoke-ADSyncDiagnostics` cmdlet은 이상 1.1.524.0 Azure AD Connect 버전에 대해서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-114">hello `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-hello-diagnostics-cmdlet"></a><span data-ttu-id="04787-115">Hello 진단 cmdlet 실행</span><span class="sxs-lookup"><span data-stu-id="04787-115">Run hello diagnostics cmdlet</span></span>
<span data-ttu-id="04787-116">tootroubleshoot 문제 암호가 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04787-116">tootroubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="04787-117">Hello로 Azure AD Connect 서버에서 새 Windows PowerShell 세션을 열고 **관리자 권한으로 실행** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="04787-117">Open a new Windows PowerShell session on your Azure AD Connect server with hello **Run as Administrator** option.</span></span>

2. <span data-ttu-id="04787-118">`Set-ExecutionPolicy RemoteSigned` 또는 `Set-ExecutionPolicy Unrestricted`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-118">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="04787-119">`Import-Module ADSyncDiagnostics`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-119">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="04787-120">`Invoke-ADSyncDiagnostics -PasswordSync`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-120">Run `Invoke-ADSyncDiagnostics -PasswordSync`.</span></span>

### <a name="understand-hello-results-of-hello-cmdlet"></a><span data-ttu-id="04787-121">Hello cmdlet의 hello 결과 이해</span><span class="sxs-lookup"><span data-stu-id="04787-121">Understand hello results of hello cmdlet</span></span>
<span data-ttu-id="04787-122">hello 진단 cmdlet는 검사를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-122">hello diagnostic cmdlet performs hello following checks:</span></span>

* <span data-ttu-id="04787-123">해당 hello의 유효성을 검사 Azure AD 테 넌 트에 대 한 암호 동기화 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-123">Validates that hello password synchronization feature is enabled for your Azure AD tenant.</span></span>

* <span data-ttu-id="04787-124">해당 hello 서버를 준비 모드에 있지 않습니다. Azure AD Connect의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-124">Validates that hello Azure AD Connect server is not in staging mode.</span></span>

* <span data-ttu-id="04787-125">각각의 기존 온-프레미스 Active Directory connector (를 기존 Active Directory 포리스트에 tooan 해당):</span><span class="sxs-lookup"><span data-stu-id="04787-125">For each existing on-premises Active Directory connector (which corresponds tooan existing Active Directory forest):</span></span>

   * <span data-ttu-id="04787-126">해당 hello의 유효성을 검사 암호 동기화 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-126">Validates that hello password synchronization feature is enabled.</span></span>
   
   * <span data-ttu-id="04787-127">Windows 응용 프로그램 이벤트 로그를 hello에서 암호 동기화 하트 비트 이벤트를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-127">Searches for password synchronization heartbeat events in hello Windows Application Event logs.</span></span>

   * <span data-ttu-id="04787-128">Hello 온-프레미스 Active Directory connector에서 각 Active Directory 도메인:</span><span class="sxs-lookup"><span data-stu-id="04787-128">For each Active Directory domain under hello on-premises Active Directory connector:</span></span>

      * <span data-ttu-id="04787-129">해당 hello의 유효성을 검사 도메인은 hello Azure AD Connect 서버에서 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-129">Validates that hello domain is reachable from hello Azure AD Connect server.</span></span>

      * <span data-ttu-id="04787-130">Hello 올바른 사용자 이름, 암호 및 암호 동기화에 필요한 사용 권한에 hello 온-프레미스 Active Directory connector에서 사용 하는 hello Active Directory 도메인 서비스 (AD DS) 계정에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-130">Validates that hello Active Directory Domain Services (AD DS) accounts used by hello on-premises Active Directory connector has hello correct username, password, and permissions required for password synchronization.</span></span>

<span data-ttu-id="04787-131">hello 다음 다이어그램에서는 단일 도메인, 온-프레미스 Active Directory 토폴로지를 hello cmdlet의 hello 결과를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="04787-131">hello following diagram illustrates hello results of hello cmdlet for a single-domain, on-premises Active Directory topology:</span></span>

![암호 동기화에 대한 진단 출력](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

<span data-ttu-id="04787-133">이 섹션의 나머지 부분 hello hello cmdlet에서 반환 되는 특정 결과 설명 및 해당 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="04787-133">hello rest of this section describes specific results that are returned by hello cmdlet and corresponding issues.</span></span>

#### <a name="password-synchronization-feature-isnt-enabled"></a><span data-ttu-id="04787-134">암호 동기화 기능이 사용되지 않음</span><span class="sxs-lookup"><span data-stu-id="04787-134">Password synchronization feature isn't enabled</span></span>
<span data-ttu-id="04787-135">Hello Azure AD Connect 마법사를 사용 하 여 암호 동기화를 활성화 하지 않은, hello 다음 오류가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04787-135">If you haven't enabled password synchronization by using hello Azure AD Connect wizard, hello following error is returned:</span></span>

![암호 동기화가 사용되지 않음](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a><span data-ttu-id="04787-137">Azure AD Connect 서버가 준비 모드에 있음</span><span class="sxs-lookup"><span data-stu-id="04787-137">Azure AD Connect server is in staging mode</span></span>
<span data-ttu-id="04787-138">Hello Azure AD Connect 서버가 준비 모드에 있으면 암호 동기화가 일시적으로 해제 하 고 hello 다음 오류가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04787-138">If hello Azure AD Connect server is in staging mode, password synchronization is temporarily disabled, and hello following error is returned:</span></span>

![Azure AD Connect 서버가 준비 모드에 있음](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a><span data-ttu-id="04787-140">암호 동기화 하트비트 이벤트 없음</span><span class="sxs-lookup"><span data-stu-id="04787-140">No password synchronization heartbeat events</span></span>
<span data-ttu-id="04787-141">각각의 온-프레미스 Active Directory 커넥터에 자체 암호 동기화 채널이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-141">Each on-premises Active Directory connector has its own password synchronization channel.</span></span> <span data-ttu-id="04787-142">Hello 암호 동기화 채널이 설정 될 때 동기화는 암호 변경 내용을 toobe 없는 하트 비트 이벤트 (이벤트 Id 654) 분 마다 한 번씩 30 hello Windows 응용 프로그램 이벤트 로그에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04787-142">When hello password synchronization channel is established and there aren't any password changes toobe synchronized, a heartbeat event (EventId 654) is generated once every 30 minutes under hello Windows Application Event Log.</span></span> <span data-ttu-id="04787-143">각 온-프레미스 Active Directory 커넥터에 대 한 hello cmdlet 검색 hello에서 해당 하트 비트 이벤트에 대 한 지난 3 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="04787-143">For each on-premises Active Directory connector, hello cmdlet searches for corresponding heartbeat events in hello past three hours.</span></span> <span data-ttu-id="04787-144">하트 비트 이벤트가 발견 되 면 hello 다음과 같은 오류가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04787-144">If no heartbeat event is found, hello following error is returned:</span></span>

![암호 동기화 하트비트 이벤트 없음](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a><span data-ttu-id="04787-146">AD DS 계정에 올바른 사용 권한이 없음</span><span class="sxs-lookup"><span data-stu-id="04787-146">AD DS account does not have correct permissions</span></span>
<span data-ttu-id="04787-147">Hello AD DS 계정 hello에서 사용 되는 온-프레미스 Active Directory connector toosynchronize 암호 해시 hello 적절 한 권한이 없을 경우 hello 다음과 같은 오류가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04787-147">If hello AD DS account that's used by hello on-premises Active Directory connector toosynchronize password hashes does not have hello appropriate permissions, hello following error is returned:</span></span>

![잘못된 자격 증명](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a><span data-ttu-id="04787-149">잘못된 AD DS 계정 사용자 이름 또는 암호</span><span class="sxs-lookup"><span data-stu-id="04787-149">Incorrect AD DS account username or password</span></span>
<span data-ttu-id="04787-150">Hello AD DS 계정에서 사용 하는 경우 hello 온-프레미스 Active Directory connector toosynchronize 암호 해시는 잘못 된 사용자 이름 또는 암호를 hello 다음 오류가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04787-150">If hello AD DS account used by hello on-premises Active Directory connector toosynchronize password hashes has an incorrect username or password, hello following error is returned:</span></span>

![잘못된 자격 증명](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-hello-diagnostic-cmdlet"></a><span data-ttu-id="04787-152">하나의 개체에 암호 동기화 되지 않는: hello 진단 cmdlet을 사용 하 여 문제 해결</span><span class="sxs-lookup"><span data-stu-id="04787-152">One object is not synchronizing passwords: troubleshoot by using hello diagnostic cmdlet</span></span>
<span data-ttu-id="04787-153">Hello를 사용할 수 있습니다 `Invoke-ADSyncDiagnostics` cmdlet toodetermine 하나의 개체만 암호 동기화 되지 않는 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="04787-153">You can use hello `Invoke-ADSyncDiagnostics` cmdlet toodetermine why one object is not synchronizing passwords.</span></span>

> [!NOTE]
> <span data-ttu-id="04787-154">hello `Invoke-ADSyncDiagnostics` cmdlet은 이상 1.1.524.0 Azure AD Connect 버전에 대해서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-154">hello `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-hello-diagnostics-cmdlet"></a><span data-ttu-id="04787-155">Hello 진단 cmdlet 실행</span><span class="sxs-lookup"><span data-stu-id="04787-155">Run hello diagnostics cmdlet</span></span>
<span data-ttu-id="04787-156">tootroubleshoot 문제 암호가 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04787-156">tootroubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="04787-157">Hello로 Azure AD Connect 서버에서 새 Windows PowerShell 세션을 열고 **관리자 권한으로 실행** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="04787-157">Open a new Windows PowerShell session on your Azure AD Connect server with hello **Run as Administrator** option.</span></span>

2. <span data-ttu-id="04787-158">`Set-ExecutionPolicy RemoteSigned` 또는 `Set-ExecutionPolicy Unrestricted`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-158">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="04787-159">`Import-Module ADSyncDiagnostics`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-159">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="04787-160">Hello 다음 cmdlet을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-160">Run hello following cmdlet:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   <span data-ttu-id="04787-161">예:</span><span class="sxs-lookup"><span data-stu-id="04787-161">For example:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-hello-results-of-hello-cmdlet"></a><span data-ttu-id="04787-162">Hello cmdlet의 hello 결과 이해</span><span class="sxs-lookup"><span data-stu-id="04787-162">Understand hello results of hello cmdlet</span></span>
<span data-ttu-id="04787-163">hello 진단 cmdlet는 검사를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-163">hello diagnostic cmdlet performs hello following checks:</span></span>

* <span data-ttu-id="04787-164">Hello Active Directory 개체에 hello Active Directory 커넥터 공간, 메타 버스 및 Azure의 hello 상태를 검사 하 여 AD 커넥터 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="04787-164">Examines hello state of hello Active Directory object in hello Active Directory connector space, Metaverse, and Azure AD connector space.</span></span>

* <span data-ttu-id="04787-165">동기화 규칙 암호 동기화와 함께 사용 하 고 toohello Active Directory 개체를 적용 합니다. 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-165">Validates that there are synchronization rules with password synchronization enabled and applied toohello Active Directory object.</span></span>

* <span data-ttu-id="04787-166">Hello 마지막 시도 toosynchronize hello에 대 한 암호 hello 개체 hello 결과 tooretrieve 및 표시를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-166">Attempts tooretrieve and display hello results of hello last attempt toosynchronize hello password for hello object.</span></span>

<span data-ttu-id="04787-167">hello 다음 다이어그램에서는 단일 개체에 대 한 암호 동기화 문제를 해결할 때 hello cmdlet의 hello 결과를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="04787-167">hello following diagram illustrates hello results of hello cmdlet when troubleshooting password synchronization for a single object:</span></span>

![암호 동기화에 대한 진단 출력 - 단일 개체](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

<span data-ttu-id="04787-169">이 섹션의 나머지 부분 hello hello cmdlet에서 반환 하는 특정 결과 설명 및 해당 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="04787-169">hello rest of this section describes specific results returned by hello cmdlet and corresponding issues.</span></span>

#### <a name="hello-active-directory-object-isnt-exported-tooazure-ad"></a><span data-ttu-id="04787-170">hello는 Active Directory 개체가 하지 않은 내보낸된 tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="04787-170">hello Active Directory object isn't exported tooAzure AD</span></span>
<span data-ttu-id="04787-171">이 온-프레미스 Active Directory 계정에 대 한 암호 동기화 hello Azure AD 테 넌 트에 해당 개체가 있기 때문에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-171">Password synchronization for this on-premises Active Directory account fails because there is no corresponding object in hello Azure AD tenant.</span></span> <span data-ttu-id="04787-172">hello 다음 오류가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04787-172">hello following error is returned:</span></span>

![Azure AD 개체가 없음](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a><span data-ttu-id="04787-174">사용자에게 임시 암호가 있음</span><span class="sxs-lookup"><span data-stu-id="04787-174">User has a temporary password</span></span>
<span data-ttu-id="04787-175">현재, Azure AD Connect는 임시 암호를 Azure AD와 동기화하는 기능을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-175">Currently, Azure AD Connect does not support synchronizing temporary passwords with Azure AD.</span></span> <span data-ttu-id="04787-176">암호를 사용 하도록 toobe 임시 경우 hello **다음 로그온 할 때 암호 변경** hello 온-프레미스 Active Directory 사용자에 옵션을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-176">A password is considered toobe temporary if hello **Change password at next logon** option is set on hello on-premises Active Directory user.</span></span> <span data-ttu-id="04787-177">hello 다음 오류가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04787-177">hello following error is returned:</span></span>

![임시 암호는 내보내지지 않음](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-toosynchronize-password-arent-available"></a><span data-ttu-id="04787-179">마지막 시도 toosynchronize 암호의 결과 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-179">Results of last attempt toosynchronize password aren't available</span></span>
<span data-ttu-id="04787-180">기본적으로 Azure AD Connect를 7 일 동안 암호 동기화 시도 hello 결과 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-180">By default, Azure AD Connect stores hello results of password synchronization attempts for seven days.</span></span> <span data-ttu-id="04787-181">Hello 선택한 Active Directory 개체에 사용할 수 없는 결과가 없는 경우 경고를 수행 하는 hello 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04787-181">If there are no results available for hello selected Active Directory object, hello following warning is returned:</span></span>

![단일 개체에 대한 진단 출력 - 암호 동기화 기록 없음](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a><span data-ttu-id="04787-183">암호가 동기화되지 않음: 수동 문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="04787-183">No passwords are synchronized: manual troubleshooting steps</span></span>
<span data-ttu-id="04787-184">이러한 단계 toodetermine 없는 암호가 동기화 되는 이유를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-184">Follow these steps toodetermine why no passwords are synchronized:</span></span>

1. <span data-ttu-id="04787-185">hello 연결 서버인 [준비 모드](active-directory-aadconnectsync-operations.md#staging-mode)?</span><span class="sxs-lookup"><span data-stu-id="04787-185">Is hello Connect server in [staging mode](active-directory-aadconnectsync-operations.md#staging-mode)?</span></span> <span data-ttu-id="04787-186">스테이징 모드의 서버는 암호를 동기화하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-186">A server in staging mode does not synchronize any passwords.</span></span>

2. <span data-ttu-id="04787-187">Hello에서 hello 스크립트를 실행 [암호 동기화 설정의 hello 상태 가져오기](#get-the-status-of-password-sync-settings) 섹션.</span><span class="sxs-lookup"><span data-stu-id="04787-187">Run hello script in hello [Get hello status of password sync settings](#get-the-status-of-password-sync-settings) section.</span></span> <span data-ttu-id="04787-188">Hello 암호 동기화 구성에 대해 간략하게를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-188">It gives you an overview of hello password sync configuration.</span></span>  

    ![암호 동기화 설정의 PowerShell 스크립트 출력](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. <span data-ttu-id="04787-190">Azure AD에서 hello 기능이 설정 되지 않은 또는 hello 동기화 채널 상태를 사용 하지 않는 경우 hello Connect 설치 마법사를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-190">If hello feature is not enabled in Azure AD or if hello sync channel status is not enabled, run hello Connect installation wizard.</span></span> <span data-ttu-id="04787-191">**동기화 옵션 사용자 지정**을 선택하고 암호 동기화의 선택을 취소합니다. 이 변경은 hello 기능을 일시적으로 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-191">Select **Customize synchronization options**, and unselect password sync. This change temporarily disables hello feature.</span></span> <span data-ttu-id="04787-192">그런 다음 hello 마법사를 다시 실행 하 고 암호 동기화를 다시 사용 하도록 설정 합니다. Hello 스크립트 실행 구성 hello tooverify 올바른지 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-192">Then run hello wizard again and re-enable password sync. Run hello script again tooverify that hello configuration is correct.</span></span>

4. <span data-ttu-id="04787-193">오류에 대 한 hello 이벤트 로그를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-193">Look in hello event log for errors.</span></span> <span data-ttu-id="04787-194">Hello 다음 문제를 나타내는 이벤트를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-194">Look for hello following events, which would indicate a problem:</span></span>
    * <span data-ttu-id="04787-195">원본: "디렉터리 동기화" ID: 0, 611, 652, 655 이러한 이벤트가 표시되면 연결 문제가 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="04787-195">Source: "Directory synchronization" ID: 0, 611, 652, 655 If you see these events, you have a connectivity problem.</span></span> <span data-ttu-id="04787-196">hello 이벤트 로그 메시지는 문제가 있는 경우 포리스트 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-196">hello event log message contains forest information where you have a problem.</span></span> <span data-ttu-id="04787-197">자세한 내용은 [연결 문제](#connectivity problem)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04787-197">For more information, see [Connectivity problem](#connectivity problem).</span></span>

5. <span data-ttu-id="04787-198">하트비트가 표시되지 않거나 아무 작동도 진행되지 않으면 [모든 암호의 전체 동기화 트리거](#trigger-a-full-sync-of-all-passwords)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-198">If you see no heartbeat or if nothing else worked, run [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span> <span data-ttu-id="04787-199">Hello 스크립트를 한 번만 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-199">Run hello script only once.</span></span>

6. <span data-ttu-id="04787-200">Hello 참조 [암호 동기화 되지 않은 한 개체의 문제를 해결](#one-object-is-not-synchronizing-passwords) 섹션.</span><span class="sxs-lookup"><span data-stu-id="04787-200">See hello [Troubleshoot one object that is not synchronizing passwords](#one-object-is-not-synchronizing-passwords) section.</span></span>

### <a name="connectivity-problems"></a><span data-ttu-id="04787-201">연결 문제</span><span class="sxs-lookup"><span data-stu-id="04787-201">Connectivity problems</span></span>

<span data-ttu-id="04787-202">Azure AD와 연결되어 있나요?</span><span class="sxs-lookup"><span data-stu-id="04787-202">Do you have connectivity with Azure AD?</span></span>

<span data-ttu-id="04787-203">Hello 계정이 모든 도메인에서 권한을 tooread hello 암호 해시를 필요한가지고?</span><span class="sxs-lookup"><span data-stu-id="04787-203">Does hello account have required permissions tooread hello password hashes in all domains?</span></span> <span data-ttu-id="04787-204">기본 설정을 사용 하 여 연결을 설치한 경우 hello 사용 권한을 이미 수정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04787-204">If you installed Connect by using Express settings, hello permissions should already be correct.</span></span> 

<span data-ttu-id="04787-205">사용자 지정 설치를 사용 하는 경우 hello 사용 권한을 수동으로 설정 hello 다음을 수행 하 여:</span><span class="sxs-lookup"><span data-stu-id="04787-205">If you used custom installation, set hello permissions manually by doing hello following:</span></span>
    
1. <span data-ttu-id="04787-206">hello Active Directory 커넥터 시작에 의해 사용 되는 toofind hello 계정 **동기화 서비스 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-206">toofind hello account used by hello Active Directory connector, start **Synchronization Service Manager**.</span></span> 
 
2. <span data-ttu-id="04787-207">너무 이동**커넥터**, 한 다음 문제를 해결 하는 hello 온-프레미스 Active Directory 포리스트 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-207">Go too**Connectors**, and then search for hello on-premises Active Directory forest you are troubleshooting.</span></span> 
 
3. <span data-ttu-id="04787-208">Hello 커넥터를 선택 하 고 클릭 한 다음 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-208">Select hello connector, and then click **Properties**.</span></span> 
 
4. <span data-ttu-id="04787-209">너무 이동**tooActive Directory 포리스트에 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-209">Go too**Connect tooActive Directory Forest**.</span></span>  
    
    ![Active Directory 커넥터에서 사용되는 계정](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    <span data-ttu-id="04787-211">Hello 사용자 이름 및 hello 계정 위치한 hello 도메인 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-211">Note hello username and hello domain where hello account is located.</span></span>
    
5. <span data-ttu-id="04787-212">시작 **Active Directory 사용자 및 컴퓨터**, 다음 이전에 발견 된 hello 계정에 포리스트의 모든 도메인의 hello 루트에 설정 된 hello 수행 권한은 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-212">Start **Active Directory Users and Computers**, and then verify that hello account you found earlier has hello follow permissions set at hello root of all domains in your forest:</span></span>
    * <span data-ttu-id="04787-213">디렉터리 변경 내용 복제</span><span class="sxs-lookup"><span data-stu-id="04787-213">Replicate Directory Changes</span></span>
    * <span data-ttu-id="04787-214">모든 디렉터리 변경 내용 복제</span><span class="sxs-lookup"><span data-stu-id="04787-214">Replicate Directory Changes All</span></span>

6. <span data-ttu-id="04787-215">Hello Azure AD Connect에서 연결할 수 있는 도메인 컨트롤러는?</span><span class="sxs-lookup"><span data-stu-id="04787-215">Are hello domain controllers reachable by Azure AD Connect?</span></span> <span data-ttu-id="04787-216">Hello 연결 서버 tooall 도메인 컨트롤러에 연결할 수 없는 경우 구성 **만 선호 도메인 컨트롤러를 사용 하 여**합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-216">If hello Connect server cannot connect tooall domain controllers, configure **Only use preferred domain controller**.</span></span>  
    
    ![Active Directory 커넥터에서 사용되는 도메인 컨트롤러](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. <span data-ttu-id="04787-218">너무 돌아가서**동기화 서비스 관리자** 및 **구성 디렉터리 파티션의**합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-218">Go back too**Synchronization Service Manager** and **Configure Directory Partition**.</span></span> 
 
8. <span data-ttu-id="04787-219">도메인을 선택 **디렉터리 파티션 선택**선택, hello **만 선호 도메인 컨트롤러를 사용 하 여** 확인란을 선택한 다음 클릭 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-219">Select your domain in **Select directory partitions**, select hello **Only use preferred domain controllers** check box, and then click **Configure**.</span></span> 

9. <span data-ttu-id="04787-220">Hello 목록에서 연결 암호 동기화에 사용 해야 하는 hello 도메인 컨트롤러를 입력 합니다. hello 동일한 목록은 가져오기 및 내보내기에도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04787-220">In hello list, enter hello domain controllers that Connect should use for password sync. hello same list is used for import and export as well.</span></span> <span data-ttu-id="04787-221">모든 도메인에 대해 이 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-221">Do these steps for all your domains.</span></span>

10. <span data-ttu-id="04787-222">Hello 스크립트 하트 비트가 임을 표시 되 면 hello 스크립트에서 실행 [모든 암호의 전체 동기화를 트리거할](#trigger-a-full-sync-of-all-passwords)합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-222">If hello script shows that there is no heartbeat, run hello script in [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span>

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a><span data-ttu-id="04787-223">한 개체가 암호를 동기화하지 않음: 수동 문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="04787-223">One object is not synchronizing passwords: manual troubleshooting steps</span></span>
<span data-ttu-id="04787-224">개체의 hello 상태를 검토 하 여 암호 동기화 문제를 쉽게 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-224">You can easily troubleshoot password synchronization issues by reviewing hello status of an object.</span></span>

1. <span data-ttu-id="04787-225">**Active Directory 사용자 및 컴퓨터**hello 사용자를 검색 한 다음 해당 hello를 확인, **사용자 다음 로그온 할 때 암호를 변경 해야** 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-225">In **Active Directory Users and Computers**, search for hello user, and then verify that hello **User must change password at next logon** check box is cleared.</span></span>  

    ![Active Directory 생산성 높은 암호](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    <span data-ttu-id="04787-227">Hello 확인란을 선택 하면 hello 사용자 toosign에 게 문의 하 고 hello 암호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-227">If hello check box is selected, ask hello user toosign in and change hello password.</span></span> <span data-ttu-id="04787-228">임시 암호는 Azure AD와 동기화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-228">Temporary passwords are not synchronized with Azure AD.</span></span>

2. <span data-ttu-id="04787-229">Hello 암호와 Active Directory에서 올바른 나타나는 경우 hello 사용자를 hello 동기화 엔진에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="04787-229">If hello password looks correct in Active Directory, follow hello user in hello sync engine.</span></span> <span data-ttu-id="04787-230">온-프레미스 Active Directory tooAzure AD에서에서 다음 hello 사용자에 의해 hello 개체에서 설명 하는 오류 인지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-230">By following hello user from on-premises Active Directory tooAzure AD, you can see whether there is a descriptive error on hello object.</span></span>

    <span data-ttu-id="04787-231">a.</span><span class="sxs-lookup"><span data-stu-id="04787-231">a.</span></span> <span data-ttu-id="04787-232">Hello 시작 [동기화 서비스 관리자](active-directory-aadconnectsync-service-manager-ui.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-232">Start hello [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span></span>

    <span data-ttu-id="04787-233">b.</span><span class="sxs-lookup"><span data-stu-id="04787-233">b.</span></span> <span data-ttu-id="04787-234">**커넥터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-234">Click **Connectors**.</span></span>

    <span data-ttu-id="04787-235">c.</span><span class="sxs-lookup"><span data-stu-id="04787-235">c.</span></span> <span data-ttu-id="04787-236">선택 hello **Active Directory Connector** hello 사용자가 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-236">Select hello **Active Directory Connector** where hello user is located.</span></span>

    <span data-ttu-id="04787-237">d.</span><span class="sxs-lookup"><span data-stu-id="04787-237">d.</span></span> <span data-ttu-id="04787-238">**커넥터 공간 검색**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-238">Select **Search Connector Space**.</span></span>

    <span data-ttu-id="04787-239">e.</span><span class="sxs-lookup"><span data-stu-id="04787-239">e.</span></span> <span data-ttu-id="04787-240">Hello에 **범위** 상자 **DN 또는 앵커**, 해결 하는 hello 사용자의 전체 DN hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-240">In hello **Scope** box, select **DN or Anchor**, and then enter hello full DN of hello user you are troubleshooting.</span></span>

    ![DN을 사용하여 커넥터 공간에서 사용자 검색](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    <span data-ttu-id="04787-242">f.</span><span class="sxs-lookup"><span data-stu-id="04787-242">f.</span></span> <span data-ttu-id="04787-243">검색 중인 하 고 클릭 hello 사용자를 찾고 **속성** toosee 모든 hello 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="04787-243">Locate hello user you are looking for, and then click **Properties** toosee all hello attributes.</span></span> <span data-ttu-id="04787-244">Hello 사용자 hello 검색 결과에 없으면 확인 프로그램 [필터링 규칙](active-directory-aadconnectsync-configure-filtering.md) 를 실행 하 고 [적용 및 변경 확인](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) 연결에서 사용자 tooappear hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-244">If hello user is not in hello search result, verify your [filtering rules](active-directory-aadconnectsync-configure-filtering.md) and make sure that you run [Apply and verify changes](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) for hello user tooappear in Connect.</span></span>

    <span data-ttu-id="04787-245">g.</span><span class="sxs-lookup"><span data-stu-id="04787-245">g.</span></span> <span data-ttu-id="04787-246">toosee hello 암호 동기화 개체의 세부 정보 hello hello에 대 한 지난 주 클릭 **로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-246">toosee hello password sync details of hello object for hello past week, click **Log**.</span></span>  

    ![개체 로그 정보](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    <span data-ttu-id="04787-248">Hello 개체 로그 비어 있으면 Azure AD Connect Active Directory에서 없습니다 tooread hello 암호 해시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-248">If hello object log is empty, Azure AD Connect has been unable tooread hello password hash from Active Directory.</span></span> <span data-ttu-id="04787-249">[연결 오류](#connectivity-errors) 문제를 계속 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-249">Continue your troubleshooting with [Connectivity Errors](#connectivity-errors).</span></span> <span data-ttu-id="04787-250">이외의 다른 값을 표시 되 면 **성공**, toohello 표에 참조 [암호 동기화 로그](#password-sync-log)합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-250">If you see any other value than **success**, refer toohello table in [Password sync log](#password-sync-log).</span></span>

    <span data-ttu-id="04787-251">h.</span><span class="sxs-lookup"><span data-stu-id="04787-251">h.</span></span> <span data-ttu-id="04787-252">선택 hello **계보** 탭을 만들고 해당 적어도 하나의 동기화 규칙 hello에 **PasswordSync** 열이 **True**합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-252">Select hello **lineage** tab, and make sure that at least one sync rule in hello **PasswordSync** column is **True**.</span></span> <span data-ttu-id="04787-253">Hello 기본 구성으로 hello hello 동기화 규칙 이름이 **에서 from AD-User AccountEnabled**합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-253">In hello default configuration, hello name of hello sync rule is **In from AD - User AccountEnabled**.</span></span>  

    ![사용자에 대한 계보 정보](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    <span data-ttu-id="04787-255">i.</span><span class="sxs-lookup"><span data-stu-id="04787-255">i.</span></span> <span data-ttu-id="04787-256">클릭 **메타 버스 개체 속성** toodisplay 사용자 특성 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="04787-256">Click **Metaverse Object Properties** toodisplay a list of user attributes.</span></span>  

    ![메타버스 정보](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    <span data-ttu-id="04787-258">**cloudFiltered** 특성이 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-258">Verify that there is no **cloudFiltered** attribute present.</span></span> <span data-ttu-id="04787-259">Hello 도메인 특성 (domainFQDN 및 domainNetBios) hello 예상 값에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-259">Make sure that hello domain attributes (domainFQDN and domainNetBios) have hello expected values.</span></span>

    <span data-ttu-id="04787-260">j.</span><span class="sxs-lookup"><span data-stu-id="04787-260">j.</span></span> <span data-ttu-id="04787-261">Hello 클릭 **커넥터** 탭 합니다. 커넥터 tooboth 온-프레미스 Active Directory를 볼 수 있어야 하 고 Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04787-261">Click hello **Connectors** tab. Make sure that you see connectors tooboth on-premises Active Directory and Azure AD.</span></span>

    ![메타버스 정보](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    <span data-ttu-id="04787-263">k.</span><span class="sxs-lookup"><span data-stu-id="04787-263">k.</span></span> <span data-ttu-id="04787-264">Azure AD를 나타내는 선택 hello 행 클릭 **속성**, hello를 클릭 한 다음 **계보** 탭 hello 커넥터 공간 개체는 아웃 바운드 규칙 hello를가지고 있어야 **PasswordSync** 열이 너무 설정**True**합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-264">Select hello row that represents Azure AD, click **Properties**, and then click hello **Lineage** tab. hello connector space object should have an outbound rule in hello **PasswordSync** column set too**True**.</span></span> <span data-ttu-id="04787-265">Hello 기본 구성으로 hello hello 동기화 규칙 이름이 **tooAAD-User Join 아웃**합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-265">In hello default configuration, hello name of hello sync rule is **Out tooAAD - User Join**.</span></span>  

    ![커넥터 공간 개체 속성 대화 상자](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a><span data-ttu-id="04787-267">암호 동기화 로그</span><span class="sxs-lookup"><span data-stu-id="04787-267">Password sync log</span></span>
<span data-ttu-id="04787-268">hello 상태 열에는 다음 값에는 hello를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-268">hello status column can have hello following values:</span></span>

| <span data-ttu-id="04787-269">가동 상태</span><span class="sxs-lookup"><span data-stu-id="04787-269">Status</span></span> | <span data-ttu-id="04787-270">설명</span><span class="sxs-lookup"><span data-stu-id="04787-270">Description</span></span> |
| --- | --- |
| <span data-ttu-id="04787-271">성공</span><span class="sxs-lookup"><span data-stu-id="04787-271">Success</span></span> |<span data-ttu-id="04787-272">암호가 성공적으로 동기화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-272">Password has been successfully synchronized.</span></span> |
| <span data-ttu-id="04787-273">FilteredByTarget</span><span class="sxs-lookup"><span data-stu-id="04787-273">FilteredByTarget</span></span> |<span data-ttu-id="04787-274">암호가 너무 설정**사용자 다음 로그온 할 때 암호를 변경 해야**합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-274">Password is set too**User must change password at next logon**.</span></span> <span data-ttu-id="04787-275">암호가 동기화되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-275">Password has not been synchronized.</span></span> |
| <span data-ttu-id="04787-276">NoTargetConnection</span><span class="sxs-lookup"><span data-stu-id="04787-276">NoTargetConnection</span></span> |<span data-ttu-id="04787-277">Hello 메타 버스의 또는 hello Azure AD 커넥터 공간에 없는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="04787-277">No object in hello metaverse or in hello Azure AD connector space.</span></span> |
| <span data-ttu-id="04787-278">SourceConnectorNotPresent</span><span class="sxs-lookup"><span data-stu-id="04787-278">SourceConnectorNotPresent</span></span> |<span data-ttu-id="04787-279">개체가 hello 온-프레미스 Active Directory 커넥터 공간에서 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-279">No object found in hello on-premises Active Directory connector space.</span></span> |
| <span data-ttu-id="04787-280">TargetNotExportedToDirectory</span><span class="sxs-lookup"><span data-stu-id="04787-280">TargetNotExportedToDirectory</span></span> |<span data-ttu-id="04787-281">Azure AD 커넥터 공간 hello에 hello 개체 아직 내보내지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-281">hello object in hello Azure AD connector space has not yet been exported.</span></span> |
| <span data-ttu-id="04787-282">MigratedCheckDetailsForMoreInfo</span><span class="sxs-lookup"><span data-stu-id="04787-282">MigratedCheckDetailsForMoreInfo</span></span> |<span data-ttu-id="04787-283">로그 항목 1.0.9125.0 빌드 전에 만들어졌으며 레거시 상태로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="04787-283">Log entry was created before build 1.0.9125.0 and is shown in its legacy state.</span></span> |
| <span data-ttu-id="04787-284">오류</span><span class="sxs-lookup"><span data-stu-id="04787-284">Error</span></span> |<span data-ttu-id="04787-285">서비스에 알 수 없는 오류가 반환되었습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-285">Service returned an unknown error.</span></span> |
| <span data-ttu-id="04787-286">알 수 없음</span><span class="sxs-lookup"><span data-stu-id="04787-286">Unknown</span></span> |<span data-ttu-id="04787-287">Tooprocess 암호 해시의 일괄 처리 하는 동안 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-287">An error occurred while trying tooprocess a batch of password hashes.</span></span>  |
| <span data-ttu-id="04787-288">MissingAttribute</span><span class="sxs-lookup"><span data-stu-id="04787-288">MissingAttribute</span></span> |<span data-ttu-id="04787-289">Azure AD Domain Services에 필요한 특정 특성(예: Kerberos 해시)을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-289">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services are not available.</span></span> |
| <span data-ttu-id="04787-290">RetryRequestedByTarget</span><span class="sxs-lookup"><span data-stu-id="04787-290">RetryRequestedByTarget</span></span> |<span data-ttu-id="04787-291">Azure AD Domain Services에 필요한 특정 특성(예: Kerberos 해시)을 이전에 사용할 수 없었습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-291">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services were not available previously.</span></span> <span data-ttu-id="04787-292">가 시도 tooresynchronize hello 사용자의 암호 해시가 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="04787-292">An attempt tooresynchronize hello user's password hash is made.</span></span> |

## <a name="scripts-toohelp-troubleshooting"></a><span data-ttu-id="04787-293">스크립트 toohelp 문제 해결</span><span class="sxs-lookup"><span data-stu-id="04787-293">Scripts toohelp troubleshooting</span></span>

### <a name="get-hello-status-of-password-sync-settings"></a><span data-ttu-id="04787-294">암호 동기화 설정의 hello 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="04787-294">Get hello status of password sync settings</span></span>
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
        Write-Warning "More than one Azure AD Connectors found. Please update hello script toouse hello appropriate Connector."
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

#### <a name="trigger-a-full-sync-of-all-passwords"></a><span data-ttu-id="04787-295">모든 암호의 전체 동기화 트리거</span><span class="sxs-lookup"><span data-stu-id="04787-295">Trigger a full sync of all passwords</span></span>
> [!NOTE]
> <span data-ttu-id="04787-296">이 스크립트는 한 번만 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-296">Run this script only once.</span></span> <span data-ttu-id="04787-297">이 두 번 이상 toorun 해야 할 경우 다른 작업은 hello 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="04787-297">If you need toorun it more than once, something else is hello problem.</span></span> <span data-ttu-id="04787-298">tootroubleshoot hello 문제를 Microsoft 지원에 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="04787-298">tootroubleshoot hello problem, contact Microsoft support.</span></span>

<span data-ttu-id="04787-299">다음 스크립트는 hello를 사용 하 여 모든 암호의 전체 동기화를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04787-299">You can trigger a full sync of all passwords by using hello following script:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="04787-300">다음 단계</span><span class="sxs-lookup"><span data-stu-id="04787-300">Next steps</span></span>
* [<span data-ttu-id="04787-301">Azure AD Connect 동기화로 암호 동기화 구현</span><span class="sxs-lookup"><span data-stu-id="04787-301">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md)
* [<span data-ttu-id="04787-302">Azure AD Connect 동기화: 동기화 옵션 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="04787-302">Azure AD Connect Sync: Customizing synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="04787-303">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="04787-303">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
