---
title: "Azure AD Connect 동기화: Azure AD Connect 동기화 서비스 계정 변경 | Microsoft Docs"
description: "이 항목 문서는 암호화 키 및 암호가 변경된 후 암호화 키를 제거하는 방법을 설명합니다."
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
ms.openlocfilehash: bf6234d0810f870909957ee1c1e33c225a4922b9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="changing-the-azure-ad-connect-sync-service-account-password"></a><span data-ttu-id="30dd2-104">Azure AD Connect 동기화 서비스 계정 암호 변경</span><span class="sxs-lookup"><span data-stu-id="30dd2-104">Changing the Azure AD Connect sync service account password</span></span>
<span data-ttu-id="30dd2-105">Azure AD Connect 동기화 서비스 계정 암호를 변경하면 암호화 키를 제거하고 Azure AD Connect 동기화 서비스 계정 암호를 다시 초기화할 때까지 동기화 서비스를 제대로 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-105">If you change the  Azure AD Connect sync service account password, the Synchronization Service will not be able start correctly until you have abandoned the encryption key and reinitialized the Azure AD Connect sync service account password.</span></span> 

<span data-ttu-id="30dd2-106">Azure AD Connect는 동기화 서비스의 일환으로 암호화 키를 사용하여 AD DS 및 Azure AD 서비스 계정의 암호를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-106">Azure AD Connect, as part of the Synchronization Services uses an encryption key to store the passwords of the AD DS and Azure AD service accounts.</span></span>  <span data-ttu-id="30dd2-107">이러한 계정은 데이터베이스에 저장되기 전에 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-107">These accounts are encrypted before they are stored in the database.</span></span> 

<span data-ttu-id="30dd2-108">사용된 암호화 키는 [Windows 데이터 보호(DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx)를 사용하여 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-108">The encryption key used is secured using [Windows Data Protection (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span></span> <span data-ttu-id="30dd2-109">DPAPI는 **Azure AD Connect 동기화 서비스 계정의 암호**를 사용하여 암호화 키를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-109">DPAPI protects the encryption key using the **password of the Azure AD Connect sync service account**.</span></span> 

<span data-ttu-id="30dd2-110">서비스 계정 암호를 변경해야 하는 경우 [Azure AD Connect 동기화 암호화 키 제거](#abandoning-the-azure-ad-connect-sync-encryption-key)의 절차를 사용하여 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-110">If you need to change the service account password you can use the procedures in [Abandoning the Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) to accomplish this.</span></span>  <span data-ttu-id="30dd2-111">이러한 절차는 어떤 이유로든 암호화 키를 제거해야 하는 경우에 사용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-111">These procedures should also be used if you need to abandon the encryption key for any reason.</span></span>

##<a name="issues-that-arise-from-changing-the-password"></a><span data-ttu-id="30dd2-112">암호 변경으로 인해 발생하는 문제</span><span class="sxs-lookup"><span data-stu-id="30dd2-112">Issues that arise from changing the password</span></span>
<span data-ttu-id="30dd2-113">서비스 계정 암호를 변경하는 경우 두 가지 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-113">There are two things that need to be done when you change the service account password.</span></span>

<span data-ttu-id="30dd2-114">첫째, Windows 서비스 제어 관리자에서 암호를 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-114">First, you need to change the password under the Windows Service Control Manager.</span></span>  <span data-ttu-id="30dd2-115">이 문제가 해결될 때까지 다음 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-115">Until this issue is resolved you will see following errors:</span></span>


- <span data-ttu-id="30dd2-116">Windows 서비스 제어 관리자에서 동기화 서비스를 시작하려고 하면 "**로컬 컴퓨터에서 Microsoft Azure AD 동기화 서비스를 시작하지 못했습니다.**"라는 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-116">If you try to start the Synchronization Service in Windows Service Control Manager, you receive the error "**Windows could not start the Microsoft Azure AD Sync service on Local Computer**".</span></span> <span data-ttu-id="30dd2-117">**오류 1069: 서비스가 로그온 실패로 인해 시작되지 않았습니다.**"</span><span class="sxs-lookup"><span data-stu-id="30dd2-117">**Error 1069: The service did not start due to a logon failure.**"</span></span>
- <span data-ttu-id="30dd2-118">Windows 이벤트 뷰어의 시스템 이벤트 로그에 **이벤트 ID 7038** “**다음 오류 때문에 현재 구성된 암호를 사용하여 ADSync 서비스에서 (으)로 로그온할 수 없습니다. 사용자 이름 또는 암호가 잘못되었습니다.**"라는 오류가 메시지가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-118">Under Windows Event Viewer, the system event log contains an error with **Event ID 7038** and message “**The ADSync service was unable to log on as with the currently configured password due to the following error: The user name or password is incorrect.**"</span></span>

<span data-ttu-id="30dd2-119">둘째, 특정 조건 하에서 암호가 업데이트되는 경우 동기화 서비스가 DPAPI를 통해 암호화 키를 더 이상 검색할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-119">Second, under specific conditions, if the password is updated, the Synchronization Service can no longer retrieve the encryption key via DPAPI.</span></span> <span data-ttu-id="30dd2-120">암호화 키가 없으면 동기화 서비스는 온-프레미스 AD 및 Azure AD 사이에서 동기화하는 데 필요한 암호를 해독할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-120">Without the encryption key, the Synchronization Service cannot decrypt the passwords required to synchronize to/from on-premises AD and Azure AD.</span></span>
<span data-ttu-id="30dd2-121">다음과 같은 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-121">You will see errors such as:</span></span>

- <span data-ttu-id="30dd2-122">Windows 서비스 제어 관리자에서 동기화 서비스를 시작하려고 하면 암호화 키를 검색할 수 없고 다음과 같은 오류로 인해 실패합니다. “**로컬 컴퓨터의 Microsoft Azure AD 동기화를 시작하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-122">Under Windows Service Control Manager, if you try to start the Synchronization Service and it cannot retrieve the encryption key, it fails with error “**Windows could not start the Microsoft Azure AD Sync on Local Computer.</span></span> <span data-ttu-id="30dd2-123">자세한 정보는 시스템 이벤트 로그를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="30dd2-123">For more information, review the System Event log.</span></span> <span data-ttu-id="30dd2-124">Microsoft 서비스가 아닌 경우, 서비스 공급업체에 문의할 때 **-21451857952**** 서비스 특정 오류를 참조하십시오.”</span><span class="sxs-lookup"><span data-stu-id="30dd2-124">If this is a non-Microsoft service, contact the service vendor, and refer to service-specific error code **-21451857952****.”</span></span>
- <span data-ttu-id="30dd2-125">Windows 이벤트 뷰어의 응용 프로그램 이벤트 로그에 **이벤트 ID 6028** *“**서버 암호화 키에 액세스할 수 없습니다.**”*라는 오류 메시지가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-125">Under Windows Event Viewer, the application event log contains an error with **Event ID 6028** and error message *“**The server encryption key cannot be accessed.**”*</span></span>

<span data-ttu-id="30dd2-126">이러한 오류가 표시되지 않도록 하려면 암호를 변경할 때 [Azure AD Connect 동기화 암호화 키 제거](#abandoning-the-azure-ad-connect-sync-encryption-key)의 절차를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="30dd2-126">To ensure that you do not receive these errors, follow the procedures in [Abandoning the Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) when changing the password.</span></span>
 
## <a name="abandoning-the-azure-ad-connect-sync-encryption-key"></a><span data-ttu-id="30dd2-127">Azure AD Connect 동기화 암호화 키 제거</span><span class="sxs-lookup"><span data-stu-id="30dd2-127">Abandoning the Azure AD Connect Sync encryption key</span></span>
>[!IMPORTANT]
><span data-ttu-id="30dd2-128">다음 절차를 Azure AD Connect 빌드 1.1.443.0 이전 빌드에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-128">The following procedures only apply to Azure AD Connect build 1.1.443.0 or older.</span></span>

<span data-ttu-id="30dd2-129">다음 절차를 사용하여 암호화 키를 제거하십시오.</span><span class="sxs-lookup"><span data-stu-id="30dd2-129">Use the following procedures to abandon the encryption key.</span></span>

### <a name="what-to-do-if-you-need-to-abandon-the-encryption-key"></a><span data-ttu-id="30dd2-130">암호화 키를 제거해야 하는 경우 수행할 작업</span><span class="sxs-lookup"><span data-stu-id="30dd2-130">What to do if you need to abandon the encryption key</span></span>

<span data-ttu-id="30dd2-131">암호화 키를 제거해야 하는 경우 다음 절차를 사용하여 작업을 수행하십시오.</span><span class="sxs-lookup"><span data-stu-id="30dd2-131">If you need to abandon the encryption key, use the following procedures to accomplish this.</span></span>

1. [<span data-ttu-id="30dd2-132">기존 암호화 키 제거</span><span class="sxs-lookup"><span data-stu-id="30dd2-132">Abandon the existing encryption key</span></span>](#abandon-the-existing-encryption-key)

2. [<span data-ttu-id="30dd2-133">AD DS 계정의 암호 제공</span><span class="sxs-lookup"><span data-stu-id="30dd2-133">Provide the password of the AD DS account</span></span>](#provide-the-password-of-the-ad-ds-account)

3. [<span data-ttu-id="30dd2-134">Azure AD 동기화 계정의 암호를 다시 초기화</span><span class="sxs-lookup"><span data-stu-id="30dd2-134">Reinitialize the password of the Azure AD sync account</span></span>](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [<span data-ttu-id="30dd2-135">동기화 서비스 시작</span><span class="sxs-lookup"><span data-stu-id="30dd2-135">Start the Synchronization Service</span></span>](#start-the-synchronization-service)

#### <a name="abandon-the-existing-encryption-key"></a><span data-ttu-id="30dd2-136">기존 암호화 키 제거</span><span class="sxs-lookup"><span data-stu-id="30dd2-136">Abandon the existing encryption key</span></span>
<span data-ttu-id="30dd2-137">새 암호화 키를 만들 수 있도록 기존 암호화 키를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-137">Abandon the existing encryption key so that new encryption key can be created:</span></span>

1. <span data-ttu-id="30dd2-138">관리자 권한으로 Azure AD Connect 서버에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-138">Log in to your Azure AD Connect Server as administrator.</span></span>

2. <span data-ttu-id="30dd2-139">새 PowerShell 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-139">Start a new PowerShell session.</span></span>

3. <span data-ttu-id="30dd2-140">`$env:Program Files\Microsoft Azure AD Sync\bin\` 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-140">Navigate to folder: `$env:Program Files\Microsoft Azure AD Sync\bin\`</span></span>

4. <span data-ttu-id="30dd2-141">`./miiskmu.exe /a` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-141">Run the command: `./miiskmu.exe /a`</span></span>

![Azure AD Connect 동기화 암호화 키 유틸리티](media/active-directory-aadconnectsync-encryption-key/key5.png)

#### <a name="provide-the-password-of-the-ad-ds-account"></a><span data-ttu-id="30dd2-143">AD DS 계정의 암호 제공</span><span class="sxs-lookup"><span data-stu-id="30dd2-143">Provide the password of the AD DS account</span></span>
<span data-ttu-id="30dd2-144">데이터베이스 내에 저장된 기존 암호를 더 이상 해독할 수 없으므로 동기화 서비스에 AD DS 계정의 암호를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-144">As the existing passwords stored inside the database can no longer be decrypted, you need to provide the Synchronization Service with the password of the AD DS account.</span></span> <span data-ttu-id="30dd2-145">동기화 서비스는 새 암호화 키를 사용하여 암호를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-145">The Synchronization Service encrypts the passwords using the new encryption key:</span></span>

1. <span data-ttu-id="30dd2-146">Synchronization Service Manager를 시작합니다(시작 → 동기화 서비스).</span><span class="sxs-lookup"><span data-stu-id="30dd2-146">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="30dd2-147">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="30dd2-147">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  
2. <span data-ttu-id="30dd2-148">**커넥터** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-148">Go to the **Connectors** tab.</span></span>
3. <span data-ttu-id="30dd2-149">온-프레미스 AD에 해당하는 **AD 커넥터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-149">Select the **AD Connector** that corresponds to your on-premises AD.</span></span> <span data-ttu-id="30dd2-150">AD 커넥터가 둘 이상이면 각각에 대해 다음 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-150">If you have more than one AD connector, repeat the following steps for each of them.</span></span>
4. <span data-ttu-id="30dd2-151">**작업** 아래에서 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-151">Under **Actions**, select **Properties**.</span></span>
5. <span data-ttu-id="30dd2-152">팝업 대화 상자에서 **Active Directory 포리스트에 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-152">In the pop-up dialog, select **Connect to Active Directory Forest**:</span></span>
6. <span data-ttu-id="30dd2-153">**암호** 텍스트 상자에 AD DS 계정의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-153">Enter the password of the AD DS account in the **Password** textbox.</span></span> <span data-ttu-id="30dd2-154">암호를 모르는 경우 이 단계를 수행하기 전에 알려진 값으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-154">If you do not know its password, you must set it to a known value before performing this step.</span></span>
7. <span data-ttu-id="30dd2-155">**확인**을 클릭하여 새 암호를 저장하고 팝업 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-155">Click **OK** to save the new password and close the pop-up dialog.</span></span>
<span data-ttu-id="30dd2-156">![Azure AD Connect 동기화 암호화 키 유틸리티](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="30dd2-156">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>

#### <a name="reinitialize-the-password-of-the-azure-ad-sync-account"></a><span data-ttu-id="30dd2-157">Azure AD 동기화 계정의 암호를 다시 초기화</span><span class="sxs-lookup"><span data-stu-id="30dd2-157">Reinitialize the password of the Azure AD sync account</span></span>
<span data-ttu-id="30dd2-158">Azure AD 서비스 계정의 암호를 동기화 서비스에 직접 제공할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-158">You cannot directly provide the password of the Azure AD service account to the Synchronization Service.</span></span> <span data-ttu-id="30dd2-159">대신 cmdlet **Add-ADSyncAADServiceAccount**을 사용하여 Azure AD 서비스 계정을 다시 초기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-159">Instead, you need to use the cmdlet **Add-ADSyncAADServiceAccount** to reinitialize the Azure AD service account.</span></span> <span data-ttu-id="30dd2-160">cmdlet은 계정 암호를 다시 설정하여 동기화 서비스에 사용할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-160">The cmdlet resets the account password and makes it available to the Synchronization Service:</span></span>

1. <span data-ttu-id="30dd2-161">Azure AD Connect 서버에서 새 PowerShell 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-161">Start a new PowerShell session on the Azure AD Connect server.</span></span>
2. <span data-ttu-id="30dd2-162">cmdlet `Add-ADSyncAADServiceAccount`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-162">Run cmdlet `Add-ADSyncAADServiceAccount`.</span></span>
3. <span data-ttu-id="30dd2-163">팝업 대화 상자에 Azure AD 테넌트에 대한 Azure AD 전역 관리자 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-163">In the pop-up dialog, provide the Azure AD Global admin credentials for your Azure AD tenant.</span></span>
<span data-ttu-id="30dd2-164">![Azure AD Connect 동기화 암호화 키 유틸리티](media/active-directory-aadconnectsync-encryption-key/key7.png)</span><span class="sxs-lookup"><span data-stu-id="30dd2-164">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key7.png)</span></span>
4. <span data-ttu-id="30dd2-165">성공한 경우 PowerShell 명령 프롬프트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-165">If it is successful, you will see the PowerShell command prompt.</span></span>

#### <a name="start-the-synchronization-service"></a><span data-ttu-id="30dd2-166">동기화 서비스 시작</span><span class="sxs-lookup"><span data-stu-id="30dd2-166">Start the Synchronization Service</span></span>
<span data-ttu-id="30dd2-167">이제 동기화 서비스가 암호화 키 및 필요한 모든 암호에 액세스할 수 있으므로 Windows 서비스 제어 관리자에서 서비스를 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-167">Now that the Synchronization Service has access to the encryption key and all the passwords it needs, you can restart the service in the Windows Service Control Manager:</span></span>


1. <span data-ttu-id="30dd2-168">Windows 서비스 제어 관리자로 이동합니다(시작 → 서비스).</span><span class="sxs-lookup"><span data-stu-id="30dd2-168">Go to Windows Service Control Manager (START → Services).</span></span>
2. <span data-ttu-id="30dd2-169">**Microsoft Azure AD 동기화**를 선택하고 다시 시작을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30dd2-169">Select **Microsoft Azure AD Sync** and click Restart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30dd2-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="30dd2-170">Next steps</span></span>
<span data-ttu-id="30dd2-171">**개요 항목**</span><span class="sxs-lookup"><span data-stu-id="30dd2-171">**Overview topics**</span></span>

* [<span data-ttu-id="30dd2-172">Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="30dd2-172">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="30dd2-173">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="30dd2-173">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
