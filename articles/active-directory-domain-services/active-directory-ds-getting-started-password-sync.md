---
title: "Azure Active Directory Domain Services: 암호 동기화 활성화 | Microsoft Docs"
description: "Azure Active Directory Domain Services 시작"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 5a32a0df-a3ca-4ebe-b980-91f58f8030fc
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 8e073df9de2996f5ad159dda746881c014ea3d66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a><span data-ttu-id="3100c-103">암호 동기화 tooAzure Active Directory 도메인 서비스를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="3100c-103">Enable password synchronization tooAzure Active Directory Domain Services</span></span>
<span data-ttu-id="3100c-104">이전 작업에서 Azure AD(Azure Active Directory) 테넌트에 대해 Azure Active Directory Domain Services를 사용하도록 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="3100c-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="3100c-105">hello 다음 작업은 관리자 NTLM (NT LAN) 및 Kerberos 인증 tooAzure에 필요한 자격 증명 해시의 tooenable 동기화 AD 도메인 서비스.</span><span class="sxs-lookup"><span data-stu-id="3100c-105">hello next task is tooenable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication tooAzure AD Domain Services.</span></span> <span data-ttu-id="3100c-106">자격 증명 동기화를 설정한 후 사용자가 회사 자격 증명으로 관리 되는 도메인 toohello 로그인 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3100c-106">After you've set up credential synchronization, users can sign in toohello managed domain with their corporate credentials.</span></span>

<span data-ttu-id="3100c-107">Azure AD Connect를 사용 하 여 온-프레미스 디렉터리에서 동기화 되는 클라우드 전용 사용자 계정 및 사용자 계정에 대 한 관련 된 hello 단계 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3100c-107">hello steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span>  <span data-ttu-id="3100c-108">Azure AD 테 넌 트의 조합은 하는 경우 사용자와 사용자가 온-프레미스에서 클라우드, AD tooperform 두 단계가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3100c-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need tooperform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="3100c-109">**클라우드 전용 사용자 계정을**: [클라우드 전용 사용자 tooyour 관리 되는 도메인 계정에 대해 암호 동기화](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="3100c-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts tooyour managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="3100c-110">**온-프레미스 사용자 계정과**: [온-프레미스에서 동기화 된 사용자 계정에 대 한 암호 동기화 할 AD tooyour 도메인 관리](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="3100c-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD tooyour managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-cloud-only-user-accounts"></a><span data-ttu-id="3100c-111">태스크 5: 암호 동기화 tooyour 클라우드 전용 사용자 계정에 대 한 관리 되는 도메인을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="3100c-111">Task 5: enable password synchronization tooyour managed domain for cloud-only user accounts</span></span>
<span data-ttu-id="3100c-112">관리 되는 도메인에 hello tooauthenticate 사용자, Azure Active Directory 도메인 서비스에는 NTLM 및 Kerberos 인증을 위해 적합 한 형식으로 해시 자격 증명 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3100c-112">tooauthenticate users on hello managed domain, Azure Active Directory Domain Services needs credential hashes in a format that's suitable for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="3100c-113">Azure AD를 생성 하지 않거나 형태로 표시 hello 테 넌 트에 대 한 Azure Active Directory 도메인 서비스를 설정할 때까지 NTLM 또는 Kerberos 인증을 하는 데 필요한 자격 증명 해시를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3100c-113">Azure AD does not generate or store credential hashes in hello format that's required for NTLM or Kerberos authentication, until you enable Azure Active Directory Domain Services for your tenant.</span></span> <span data-ttu-id="3100c-114">확실한 보안상의 이유로 Azure AD는 암호 자격 증명을 일반 텍스트 형식으로 저장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3100c-114">For obvious security reasons, Azure AD also does not store any password credentials in clear-text form.</span></span> <span data-ttu-id="3100c-115">따라서 Azure AD 사용자의 기존 자격 증명에 따라 이러한 NTLM 또는 Kerberos 자격 증명 해시를 생성 하는 방식으로 tooautomatically가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3100c-115">Therefore, Azure AD does not have a way tooautomatically generate these NTLM or Kerberos credential hashes based on users' existing credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="3100c-116">조직에 클라우드 전용 사용자 계정이 있는 경우 toouse Azure Active Directory 도메인 서비스를 해야 하는 사용자가 암호를 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3100c-116">If your organization has cloud-only user accounts, users who need toouse Azure Active Directory Domain Services must change their passwords.</span></span> <span data-ttu-id="3100c-117">클라우드 전용 사용자 계정에는 hello Azure 포털 또는 Azure AD PowerShell cmdlet 중 하나를 사용 하 여 Azure AD 디렉터리에서 만든 계정이입니다.</span><span class="sxs-lookup"><span data-stu-id="3100c-117">A cloud-only user account is an account that was created in your Azure AD directory using either hello Azure portal or Azure AD PowerShell cmdlets.</span></span> <span data-ttu-id="3100c-118">이러한 사용자 계정은 온-프레미스 디렉터리에서 동기화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3100c-118">Such user accounts aren't synchronized from an on-premises directory.</span></span>
>
>

<span data-ttu-id="3100c-119">이 암호 변경 프로세스는 hello 자격 증명은 Azure AD에서 생성 하는 Kerberos 및 NTLM 인증 toobe에 대 한 Azure Active Directory 도메인 서비스에 필요한 해시 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3100c-119">This password change process causes hello credential hashes that are required by Azure Active Directory Domain Services for Kerberos and NTLM authentication toobe generated in Azure AD.</span></span> <span data-ttu-id="3100c-120">Hello에서 모든 사용자 toouse Azure Active Directory 도메인 서비스를 해야 하는 테 넌 트 또는 toochange 지시에 대 한 hello 암호 만료 되거나 수는 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="3100c-120">You can either expire hello passwords for all users in hello tenant who need toouse Azure Active Directory Domain Services or instruct them toochange their passwords.</span></span>

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a><span data-ttu-id="3100c-121">클라우드 전용 사용자 계정에 대해 NTLM 및 Kerberos 자격 증명 해시 생성 사용</span><span class="sxs-lookup"><span data-stu-id="3100c-121">Enable NTLM and Kerberos credential hash generation for a cloud-only user account</span></span>
<span data-ttu-id="3100c-122">Hello 지침 tooprovide 사용자가 암호를 변경할 수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3100c-122">Here are hello instructions you need tooprovide users, so they can change their passwords:</span></span>

1. <span data-ttu-id="3100c-123">Toohello 이동 [Azure AD 액세스 패널](http://myapps.microsoft.com) त ा.</span><span class="sxs-lookup"><span data-stu-id="3100c-123">Go toohello [Azure AD Access Panel](http://myapps.microsoft.com) page for your organization.</span></span>

    ![Hello Azure AD 액세스 패널을 시작 합니다.](./media/active-directory-domain-services-getting-started/access-panel.png)

2. <span data-ttu-id="3100c-125">Hello 오른쪽 위의 모서리에서 이름을 클릭 하 고 선택 **프로필** hello 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3100c-125">In hello top right corner, click on your name and select **Profile** from hello menu.</span></span>

    ![프로필 선택](./media/active-directory-domain-services-getting-started/select-profile.png)

3. <span data-ttu-id="3100c-127">Hello에 **프로필** 페이지에서 클릭 **암호 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="3100c-127">On hello **Profile** page, click on **Change password**.</span></span>

    !["암호 변경" 클릭](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > <span data-ttu-id="3100c-129">경우 hello **암호 변경** hello 액세스 패널 창에 옵션이 표시 되지 않습니다, 조직에서 구성한 확인 [Azure AD의 암호 관리](../active-directory/active-directory-passwords-getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3100c-129">If hello **Change password** option is not displayed in hello Access Panel window, ensure that your organization has configured [password management in Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span></span>
   >
   >
4. <span data-ttu-id="3100c-130">Hello에 **암호 변경** 페이지, 기존 (현재) 암호를 입력 하 고, 새 암호를 입력 하 고 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3100c-130">On hello **change password** page, type your existing (old) password, type a new password, and then confirm it.</span></span>

    ![Azure AD 도메인 서비스에 대한 가상 네트워크를 만듭니다.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. <span data-ttu-id="3100c-132">**제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3100c-132">Click **submit**.</span></span>

<span data-ttu-id="3100c-133">암호를 변경한 후 몇 분이 hello 새 암호는 Azure Active Directory 도메인 서비스에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3100c-133">A few minutes after you have changed your password, hello new password is usable in Azure Active Directory Domain Services.</span></span> <span data-ttu-id="3100c-134">몇 분 후 (일반적으로 약 20 분) hello 새로 변경 된 암호를 사용 하 여 관리 되는 도메인 조인된 toohello 있는 toocomputers 로그인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3100c-134">After a few more minutes (typically, about 20 minutes), you can sign in toocomputers that are joined toohello managed domain by using hello newly changed password.</span></span>

## <a name="related-content"></a><span data-ttu-id="3100c-135">관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="3100c-135">Related Content</span></span>
* [<span data-ttu-id="3100c-136">어떻게 tooupdate 암호</span><span class="sxs-lookup"><span data-stu-id="3100c-136">How tooupdate your own password</span></span>](../active-directory/active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="3100c-137">Azure AD에서 암호 관리 시작</span><span class="sxs-lookup"><span data-stu-id="3100c-137">Getting started with Password Management in Azure AD</span></span>](../active-directory/active-directory-passwords-getting-started.md)
* [<span data-ttu-id="3100c-138">암호 동기화 사용 tooAzure Active Directory 도메인 서비스에 대 한 동기화 된 Azure AD 테 넌 트</span><span class="sxs-lookup"><span data-stu-id="3100c-138">Enable password synchronization tooAzure Active Directory Domain Services for a synced Azure AD tenant</span></span>](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [<span data-ttu-id="3100c-139">Azure Active Directory Domain Services 관리되는 도메인 관리</span><span class="sxs-lookup"><span data-stu-id="3100c-139">Administer an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="3100c-140">Windows 가상 컴퓨터 tooan Azure Active Directory 도메인 서비스에서 관리 하는 도메인에 가입</span><span class="sxs-lookup"><span data-stu-id="3100c-140">Join a Windows virtual machine tooan Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="3100c-141">Red Hat Enterprise Linux 가상 컴퓨터 tooan Azure Active Directory 도메인 서비스에서 관리 하는 도메인에 가입</span><span class="sxs-lookup"><span data-stu-id="3100c-141">Join a Red Hat Enterprise Linux virtual machine tooan Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
