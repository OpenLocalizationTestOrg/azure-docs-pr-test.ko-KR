---
title: "Azure AD Connect 동기화: hello Azure AD 연결 동기화 서비스 계정 변경 | Microsoft Docs"
description: "항목 설명 hello 암호화 키 및 tooabandon hello 암호 후 방법은 변경 합니다."
services: active-directory
keywords: "Azure AD 동기화 서비스 계정, 암호"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 11948ac4662f722e4f684ef6c9b9ccdc6387e60f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-azure-ad-connect-sync-service-account-password"></a><span data-ttu-id="88fc7-104">Hello Azure AD Connect 동기화 서비스 계정 암호 변경</span><span class="sxs-lookup"><span data-stu-id="88fc7-104">Changing hello Azure AD Connect sync service account password</span></span>
<span data-ttu-id="88fc7-105">Hello Azure AD Connect 동기화 서비스 계정 암호를 변경 하면 hello 동기화 서비스 됩니다 수 시작 올바르게 hello 암호화 키를 중단 하 고 hello Azure AD Connect 동기화 서비스 계정 암호를 다시 초기화 될 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-105">If you change hello  Azure AD Connect sync service account password, hello Synchronization Service will not be able start correctly until you have abandoned hello encryption key and reinitialized hello Azure AD Connect sync service account password.</span></span> 

<span data-ttu-id="88fc7-106">Azure AD Connect hello 동기화 서비스의 일부로 hello AD DS와 Azure AD 서비스 계정을 암호화 키 toostore hello 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-106">Azure AD Connect, as part of hello Synchronization Services uses an encryption key toostore hello passwords of hello AD DS and Azure AD service accounts.</span></span>  <span data-ttu-id="88fc7-107">이러한 계정은 hello 데이터베이스에 저장 되기 전에 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-107">These accounts are encrypted before they are stored in hello database.</span></span> 

<span data-ttu-id="88fc7-108">hello 사용 되는 암호화 키로 보호 될 [Windows DPAPI (데이터 보호)](https://msdn.microsoft.com/library/ms995355.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-108">hello encryption key used is secured using [Windows Data Protection (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span></span> <span data-ttu-id="88fc7-109">Hello를 사용 하 여 hello 암호화 키를 보호 하는 DPAPI **hello Azure AD Connect 동기화 서비스 계정 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-109">DPAPI protects hello encryption key using hello **password of hello Azure AD Connect sync service account**.</span></span> 

<span data-ttu-id="88fc7-110">hello 절차를 사용할 수 toochange hello 서비스 계정 암호가 필요한 경우 [Abandoning hello Azure AD Sync 연결 암호화 키](#abandoning-the-azure-ad-connect-sync-encryption-key) tooaccomplish이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-110">If you need toochange hello service account password you can use hello procedures in [Abandoning hello Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) tooaccomplish this.</span></span>  <span data-ttu-id="88fc7-111">또한 어떤 이유로 든 tooabandon hello 암호화 키가 필요한 경우 이러한 절차를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-111">These procedures should also be used if you need tooabandon hello encryption key for any reason.</span></span>

##<a name="issues-that-arise-from-changing-hello-password"></a><span data-ttu-id="88fc7-112">Hello 암호 변경에서 발생 하는 문제</span><span class="sxs-lookup"><span data-stu-id="88fc7-112">Issues that arise from changing hello password</span></span>
<span data-ttu-id="88fc7-113">Toobe hello 서비스 계정 암호를 변경 하는 경우 수행 해야 하는 두 가지입니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-113">There are two things that need toobe done when you change hello service account password.</span></span>

<span data-ttu-id="88fc7-114">먼저 hello Windows 서비스 제어 관리자에서 toochange hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-114">First, you need toochange hello password under hello Windows Service Control Manager.</span></span>  <span data-ttu-id="88fc7-115">이 문제가 해결될 때까지 다음 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-115">Until this issue is resolved you will see following errors:</span></span>


- <span data-ttu-id="88fc7-116">Hello 오류가 나타나면 toostart hello 동기화 서비스 Windows 서비스 제어 관리자에서 시도 하면 "**로컬 컴퓨터에서 Windows hello Microsoft Azure AD Sync 서비스를 시작 하지 못했습니다**"입니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-116">If you try toostart hello Synchronization Service in Windows Service Control Manager, you receive hello error "**Windows could not start hello Microsoft Azure AD Sync service on Local Computer**".</span></span> <span data-ttu-id="88fc7-117">**오류 1069: hello 서비스 tooa 로그온 실패로 인해 시작 되지 않았습니다.** "</span><span class="sxs-lookup"><span data-stu-id="88fc7-117">**Error 1069: hello service did not start due tooa logon failure.**"</span></span>
- <span data-ttu-id="88fc7-118">Hello 시스템 이벤트 로그에서 Windows 이벤트 뷰어 오류가 포함 되어 **이벤트 ID 7038** 및 메시지 "**hello ADSync 서비스에 없습니다 toolog toohello 다음 인해 hello 현재 구성 된 암호와 마찬가지로 된 오류: hello 사용자 이름 또는 암호가 올바르지 않습니다.** "</span><span class="sxs-lookup"><span data-stu-id="88fc7-118">Under Windows Event Viewer, hello system event log contains an error with **Event ID 7038** and message “**hello ADSync service was unable toolog on as with hello currently configured password due toohello following error: hello user name or password is incorrect.**"</span></span>

<span data-ttu-id="88fc7-119">둘째, 특정 조건에서 hello 암호 업데이트 되 면 hello 동기화 서비스가 더 이상 검색할 수 DPAPI 통해 hello 암호화 키.</span><span class="sxs-lookup"><span data-stu-id="88fc7-119">Second, under specific conditions, if hello password is updated, hello Synchronization Service can no longer retrieve hello encryption key via DPAPI.</span></span> <span data-ttu-id="88fc7-120">Hello 암호화 키가 없으면 동기화 서비스 hello 필요한 toosynchronize로 /에서 암호를 해독할 수 없음 hello 온-프레미스 AD와 Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88fc7-120">Without hello encryption key, hello Synchronization Service cannot decrypt hello passwords required toosynchronize to/from on-premises AD and Azure AD.</span></span>
<span data-ttu-id="88fc7-121">다음과 같은 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-121">You will see errors such as:</span></span>

- <span data-ttu-id="88fc7-122">Windows 서비스 제어 관리자에서 toostart hello 동기화 서비스는 hello 암호화 키를 검색할 수 없는 경우 요청이 실패 오류 "* * 로컬 컴퓨터에서 Windows hello Microsoft Azure AD Sync를 시작 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-122">Under Windows Service Control Manager, if you try toostart hello Synchronization Service and it cannot retrieve hello encryption key, it fails with error “**Windows could not start hello Microsoft Azure AD Sync on Local Computer.</span></span> <span data-ttu-id="88fc7-123">자세한 내용은 hello 시스템 이벤트 로그를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-123">For more information, review hello System Event log.</span></span> <span data-ttu-id="88fc7-124">이 타사 서비스 hello 서비스 공급 업체에 문의 한 tooservice 요소별 오류 코드를 참조 하십시오. * *-21451857952 * * *. "</span><span class="sxs-lookup"><span data-stu-id="88fc7-124">If this is a non-Microsoft service, contact hello service vendor, and refer tooservice-specific error code **-21451857952****.”</span></span>
- <span data-ttu-id="88fc7-125">Hello 응용 프로그램 이벤트 로그에서 Windows 이벤트 뷰어 오류가 포함 되어 **이벤트 ID 6028** 및 오류 메시지 *"**hello 서버 암호화 키에 액세스할 수 없습니다.* *"*</span><span class="sxs-lookup"><span data-stu-id="88fc7-125">Under Windows Event Viewer, hello application event log contains an error with **Event ID 6028** and error message *“**hello server encryption key cannot be accessed.**”*</span></span>

<span data-ttu-id="88fc7-126">이러한 오류를 수신 하지 않는 tooensure에 hello 절차에 따라 [Abandoning hello Azure AD Sync 연결 암호화 키](#abandoning-the-azure-ad-connect-sync-encryption-key) hello 암호를 변경 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="88fc7-126">tooensure that you do not receive these errors, follow hello procedures in [Abandoning hello Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) when changing hello password.</span></span>
 
## <a name="abandoning-hello-azure-ad-connect-sync-encryption-key"></a><span data-ttu-id="88fc7-127">암호화 키를 Azure AD 연결 동기화 하는 hello를 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-127">Abandoning hello Azure AD Connect Sync encryption key</span></span>
>[!IMPORTANT]
><span data-ttu-id="88fc7-128">hello 다음 절차만 적용 tooAzure AD Connect 빌드 1.1.443.0 또는 이전 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-128">hello following procedures only apply tooAzure AD Connect build 1.1.443.0 or older.</span></span>

<span data-ttu-id="88fc7-129">다음 프로시저 tooabandon hello 암호화 키 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-129">Use hello following procedures tooabandon hello encryption key.</span></span>

### <a name="what-toodo-if-you-need-tooabandon-hello-encryption-key"></a><span data-ttu-id="88fc7-130">어떤 toodo tooabandon hello 암호화 키가 필요한 경우</span><span class="sxs-lookup"><span data-stu-id="88fc7-130">What toodo if you need tooabandon hello encryption key</span></span>

<span data-ttu-id="88fc7-131">필요한 경우 tooabandon hello 암호화 키를 사용 프로시저 tooaccomplish 다음 hello이 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-131">If you need tooabandon hello encryption key, use hello following procedures tooaccomplish this.</span></span>

1. [<span data-ttu-id="88fc7-132">Hello 기존 암호화 키를 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-132">Abandon hello existing encryption key</span></span>](#abandon-the-existing-encryption-key)

2. [<span data-ttu-id="88fc7-133">AD DS 계정 hello hello 암호 제공</span><span class="sxs-lookup"><span data-stu-id="88fc7-133">Provide hello password of hello AD DS account</span></span>](#provide-the-password-of-the-ad-ds-account)

3. [<span data-ttu-id="88fc7-134">Azure AD 동기화 계정 hello의 hello 암호를 다시 초기화</span><span class="sxs-lookup"><span data-stu-id="88fc7-134">Reinitialize hello password of hello Azure AD sync account</span></span>](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [<span data-ttu-id="88fc7-135">Hello 동기화 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-135">Start hello Synchronization Service</span></span>](#start-the-synchronization-service)

#### <a name="abandon-hello-existing-encryption-key"></a><span data-ttu-id="88fc7-136">Hello 기존 암호화 키를 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-136">Abandon hello existing encryption key</span></span>
<span data-ttu-id="88fc7-137">Hello 기존 암호화 키를 중단 하는 새로운 암호화 키를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-137">Abandon hello existing encryption key so that new encryption key can be created:</span></span>

1. <span data-ttu-id="88fc7-138">관리자 권한으로 Azure AD 연결 서버 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-138">Log in tooyour Azure AD Connect Server as administrator.</span></span>

2. <span data-ttu-id="88fc7-139">새 PowerShell 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-139">Start a new PowerShell session.</span></span>

3. <span data-ttu-id="88fc7-140">Toofolder를 이동 합니다.`$env:Program Files\Microsoft Azure AD Sync\bin\`</span><span class="sxs-lookup"><span data-stu-id="88fc7-140">Navigate toofolder: `$env:Program Files\Microsoft Azure AD Sync\bin\`</span></span>

4. <span data-ttu-id="88fc7-141">Hello 명령을 실행 합니다.`./miiskmu.exe /a`</span><span class="sxs-lookup"><span data-stu-id="88fc7-141">Run hello command: `./miiskmu.exe /a`</span></span>

![Azure AD Connect 동기화 암호화 키 유틸리티](media/active-directory-aadconnectsync-encryption-key/key5.png)

#### <a name="provide-hello-password-of-hello-ad-ds-account"></a><span data-ttu-id="88fc7-143">AD DS 계정 hello hello 암호 제공</span><span class="sxs-lookup"><span data-stu-id="88fc7-143">Provide hello password of hello AD DS account</span></span>
<span data-ttu-id="88fc7-144">Hello 데이터베이스 내에 저장 하는 hello 기존 암호를 해독할 수 없습니다, AD DS hello 계정의 hello 암호로 tooprovide hello 동기화 서비스 필요.</span><span class="sxs-lookup"><span data-stu-id="88fc7-144">As hello existing passwords stored inside hello database can no longer be decrypted, you need tooprovide hello Synchronization Service with hello password of hello AD DS account.</span></span> <span data-ttu-id="88fc7-145">hello 새 암호화 키를 사용 하 여 hello 암호를 암호화 하는 hello 동기화 서비스:</span><span class="sxs-lookup"><span data-stu-id="88fc7-145">hello Synchronization Service encrypts hello passwords using hello new encryption key:</span></span>

1. <span data-ttu-id="88fc7-146">Hello 동기화 서비스 관리자 (→ 시작 동기화 서비스)를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-146">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="88fc7-147">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="88fc7-147">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  
2. <span data-ttu-id="88fc7-148">Toohello 이동 **커넥터** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-148">Go toohello **Connectors** tab.</span></span>
3. <span data-ttu-id="88fc7-149">선택 hello **AD 커넥터** tooyour 해당 하는 온-프레미스 AD 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-149">Select hello **AD Connector** that corresponds tooyour on-premises AD.</span></span> <span data-ttu-id="88fc7-150">둘 이상의 AD 커넥터를 설정한 경우 hello 각각의 다음 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-150">If you have more than one AD connector, repeat hello following steps for each of them.</span></span>
4. <span data-ttu-id="88fc7-151">**작업** 아래에서 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-151">Under **Actions**, select **Properties**.</span></span>
5. <span data-ttu-id="88fc7-152">Hello 팝업 대화 상자에서 선택 **tooActive Directory 포리스트에 연결**:</span><span class="sxs-lookup"><span data-stu-id="88fc7-152">In hello pop-up dialog, select **Connect tooActive Directory Forest**:</span></span>
6. <span data-ttu-id="88fc7-153">Hello에 AD DS hello 계정의 hello 암호를 입력 **암호** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-153">Enter hello password of hello AD DS account in hello **Password** textbox.</span></span> <span data-ttu-id="88fc7-154">암호를 모르는 경우이 단계를 수행 하기 전에 값을 알려진 tooa를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-154">If you do not know its password, you must set it tooa known value before performing this step.</span></span>
7. <span data-ttu-id="88fc7-155">클릭 **확인** toosave hello 새 암호와 닫기 hello 팝업 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="88fc7-155">Click **OK** toosave hello new password and close hello pop-up dialog.</span></span>
<span data-ttu-id="88fc7-156">![Azure AD Connect 동기화 암호화 키 유틸리티](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="88fc7-156">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>

#### <a name="reinitialize-hello-password-of-hello-azure-ad-sync-account"></a><span data-ttu-id="88fc7-157">Azure AD 동기화 계정 hello의 hello 암호를 다시 초기화</span><span class="sxs-lookup"><span data-stu-id="88fc7-157">Reinitialize hello password of hello Azure AD sync account</span></span>
<span data-ttu-id="88fc7-158">직접 hello Azure AD 서비스 계정 toohello 동기화 서비스의 hello 암호를 제공할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-158">You cannot directly provide hello password of hello Azure AD service account toohello Synchronization Service.</span></span> <span data-ttu-id="88fc7-159">대신, toouse hello cmdlet 필요 **추가 ADSyncAADServiceAccount** tooreinitialize hello Azure AD 서비스 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-159">Instead, you need toouse hello cmdlet **Add-ADSyncAADServiceAccount** tooreinitialize hello Azure AD service account.</span></span> <span data-ttu-id="88fc7-160">hello cmdlet hello 계정 암호를 재설정 하 고 사용할 수 있는 toohello 동기화 서비스를 사용 하면:</span><span class="sxs-lookup"><span data-stu-id="88fc7-160">hello cmdlet resets hello account password and makes it available toohello Synchronization Service:</span></span>

1. <span data-ttu-id="88fc7-161">Hello Azure AD Connect 서버에서 새 PowerShell 세션을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-161">Start a new PowerShell session on hello Azure AD Connect server.</span></span>
2. <span data-ttu-id="88fc7-162">cmdlet `Add-ADSyncAADServiceAccount`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-162">Run cmdlet `Add-ADSyncAADServiceAccount`.</span></span>
3. <span data-ttu-id="88fc7-163">Hello 팝업 대화 상자에서 Azure AD 테 넌 트에 대 한 hello Azure AD 전역 관리자 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-163">In hello pop-up dialog, provide hello Azure AD Global admin credentials for your Azure AD tenant.</span></span>
<span data-ttu-id="88fc7-164">![Azure AD Connect 동기화 암호화 키 유틸리티](media/active-directory-aadconnectsync-encryption-key/key7.png)</span><span class="sxs-lookup"><span data-stu-id="88fc7-164">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key7.png)</span></span>
4. <span data-ttu-id="88fc7-165">성공한 경우에 hello PowerShell 명령 프롬프트를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-165">If it is successful, you will see hello PowerShell command prompt.</span></span>

#### <a name="start-hello-synchronization-service"></a><span data-ttu-id="88fc7-166">Hello 동기화 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-166">Start hello Synchronization Service</span></span>
<span data-ttu-id="88fc7-167">Hello 동기화 서비스에 대 한 액세스 toohello 암호화 키 및 암호를 hello 모든 했으므로, hello Windows 서비스 제어 관리자에서에서 hello 서비스를 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-167">Now that hello Synchronization Service has access toohello encryption key and all hello passwords it needs, you can restart hello service in hello Windows Service Control Manager:</span></span>


1. <span data-ttu-id="88fc7-168">TooWindows 서비스 제어 관리자 (시작 → 서비스)를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-168">Go tooWindows Service Control Manager (START → Services).</span></span>
2. <span data-ttu-id="88fc7-169">**Microsoft Azure AD 동기화**를 선택하고 다시 시작을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc7-169">Select **Microsoft Azure AD Sync** and click Restart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88fc7-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="88fc7-170">Next steps</span></span>
<span data-ttu-id="88fc7-171">**개요 항목**</span><span class="sxs-lookup"><span data-stu-id="88fc7-171">**Overview topics**</span></span>

* [<span data-ttu-id="88fc7-172">Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="88fc7-172">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="88fc7-173">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="88fc7-173">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
