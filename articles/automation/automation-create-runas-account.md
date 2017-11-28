---
title: "Azure 자동화 계정으로 실행 계정 aaaCreate | Microsoft Docs"
description: "이 문서에서는 설명 방법을 tooupdate 자동화 계정 및 hello 포털 또는 powershell을 실행 계정을 만듭니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: magoedte
ms.openlocfilehash: 94eb54fa0b518056a726d17146c63411e248273b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-automation-account-authentication-with-run-as-accounts"></a><span data-ttu-id="4810a-103">실행 계정으로 Automation 계정 인증 업데이트</span><span class="sxs-lookup"><span data-stu-id="4810a-103">Update your Automation account authentication with Run As accounts</span></span> 
<span data-ttu-id="4810a-104">Hello 포털에서 기존 자동화 계정을 업데이트 하거나 경우 PowerShell을 사용 하 여 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-104">You can update your existing Automation account from hello portal or use PowerShell if:</span></span>

* <span data-ttu-id="4810a-105">자동화 계정을 만들지만 toocreate hello 계정으로 실행을 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-105">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="4810a-106">자동화 계정 toomanage 리소스 관리자 리소스를 이미 사용 중이 고 tooupdate hello 계정 tooinclude hello 실행 계정을 runbook 인증에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-106">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="4810a-107">자동화 계정 toomanage 클래식 리소스를 이미 사용 중이 고 tooupdate 것 toouse hello 클래식 실행 계정 대신 새 계정을 만들고 runbook과 자산 tooit 마이그레이션.</span><span class="sxs-lookup"><span data-stu-id="4810a-107">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="4810a-108">Toocreate 실행 하 고 기본 실행 계정을 사용 하 여 원하는 엔터프라이즈 인증 기관 (CA)에서 발급 한 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-108">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4810a-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4810a-109">Prerequisites</span></span>

* <span data-ttu-id="4810a-110">Azure 리소스 관리자 모듈 3.0.0 때 Windows 10 및 Windows Server 2016에만 실행 이상을 hello 스크립트 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-110">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 3.0.0 and later.</span></span> <span data-ttu-id="4810a-111">이전 버전의 Windows에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="4810a-112">Azure PowerShell 1.0 이상</span><span class="sxs-lookup"><span data-stu-id="4810a-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="4810a-113">PowerShell 1.0 hello 릴리스에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azureps-cmdlets-docs)합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-113">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="4810a-114">Hello에 대 한 hello 값으로 참조 하는 자동화 계정을 *– AutomationAccountName* 및 *-ApplicationDisplayName* hello PowerShell 스크립트 뒤에 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-114">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="4810a-115">tooget hello에 대 한 값 *SubscriptionID*, *ResourceGroup*, 및 *AutomationAccountName*, hello 스크립트에 대 한 필수 매개 변수는, 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-115">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello script, do hello following:</span></span>

1. <span data-ttu-id="4810a-116">Hello Azure 포털에서 hello에서 자동화 계정을 선택 **자동화 계정** 블레이드에서 다음을 선택 하 고 **모든 설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-116">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span>  
2. <span data-ttu-id="4810a-117">Hello에 **모든 설정을** 블레이드 아래 **계정 설정**선택, **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-117">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="4810a-118">Hello에 hello 값을 기록 **속성** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-118">Note hello values on hello **Properties** blade.</span></span><br><br> <span data-ttu-id="4810a-119">![hello 자동화 계정 "속성" 블레이드](media/automation-create-runas-account/automation-account-properties.png)</span><span class="sxs-lookup"><span data-stu-id="4810a-119">![hello Automation account "Properties" blade](media/automation-create-runas-account/automation-account-properties.png)</span></span>  

### <a name="required-permissions-tooupdate-your-automation-account"></a><span data-ttu-id="4810a-120">필요한 사용 권한을 tooupdate 자동화 계정</span><span class="sxs-lookup"><span data-stu-id="4810a-120">Required permissions tooupdate your Automation account</span></span>
<span data-ttu-id="4810a-121">자동화 계정을 tooupdate 있어야 다음 특정 권한을 hello 및이 항목 toocomplete 필요한 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="4810a-121">tooupdate an Automation account, you must have hello following specific privileges and permissions required toocomplete this topic.</span></span>   
 
* <span data-ttu-id="4810a-122">AD 사용자 계정의 Microsoft.Automation 리소스에 대 한 사용 권한 해당 toohello 참가자 역할을 가진 toobe 추가 tooa 역할 문서에 설명 된 대로 필요한 [Azure 자동화에서 역할 기반 액세스 제어](automation-role-based-access-control.md#contributor-role-permissions)합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-122">Your AD user account needs toobe added tooa role with permissions equivalent toohello Contributor role for Microsoft.Automation resources as outlined in article [Role-based access control in Azure Automation](automation-role-based-access-control.md#contributor-role-permissions).</span></span>  
* <span data-ttu-id="4810a-123">Azure AD 테 넌 트의 관리자가 아닌 사용자 수 [AD 응용 프로그램 등록](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) hello 응용 프로그램 등록 설정 너무 설정 되어 있으면**예**합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-123">Non-admin users in your Azure AD tenant can [register AD applications](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) if hello App registrations setting is set too**Yes**.</span></span>  <span data-ttu-id="4810a-124">Hello 응용 프로그램 등록 설정 너무 설정 되어 있으면**아니요**,이 작업을 수행 하는 hello 사용자는 Azure ad에서 전역 관리자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-124">If hello app registrations setting is set too**No**, hello user performing this action must be a global administrator in Azure AD.</span></span> 

<span data-ttu-id="4810a-125">가 아닌 hello 구독 Active Directory 인스턴스에서 소속 toohello 전역 관리자/공동 관리자의 역할 hello 구독을 추가 하기 전에 사용자 tooActive 디렉터리에 게스트로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-125">If you are not a member of hello subscription’s Active Directory instance before you are added toohello global administrator/co-administrator role of hello subscription, you are added tooActive Directory as a guest.</span></span> <span data-ttu-id="4810a-126">이 경우에는 "없는 사용 권한을 toocreate..." 표시</span><span class="sxs-lookup"><span data-stu-id="4810a-126">In this situation, you receive a “You do not have permissions toocreate…”</span></span> <span data-ttu-id="4810a-127">hello에 경고 **자동화 계정 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-127">warning on hello **Add Automation Account** blade.</span></span> <span data-ttu-id="4810a-128">먼저 hello 구독 Active Directory 인스턴스에서 제거할 수도 있고 toomake 다시 추가 toohello 전역 관리자/공동 관리자 역할에 추가 된 사용자를 해당 Active Directory에서 전체 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-128">Users who were added toohello global administrator/co-administrator role first can be removed from hello subscription's Active Directory instance and re-added toomake them a full User in Active Directory.</span></span> <span data-ttu-id="4810a-129">tooverify hello에서 이러한 경우 **Azure Active Directory** hello Azure 포털의에서 창 **사용자 및 그룹**선택, **모든 사용자에 게** 및 hello를 선택한 후 특정 사용자 **프로필**합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-129">tooverify this situation, from hello **Azure Active Directory** pane in hello Azure portal, select **Users and groups**, select **All users** and, after you select hello specific user, select **Profile**.</span></span> <span data-ttu-id="4810a-130">값의 hello hello **사용자 유형** hello 사용자 프로필 아래에 특성 같지 해야 **게스트**합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-130">hello value of hello **User type** attribute under hello users profile should not equal **Guest**.</span></span>

## <a name="create-run-as-account-from-hello-portal"></a><span data-ttu-id="4810a-131">Hello 포털에서 다음 계정으로 실행 계정을 만들려면</span><span class="sxs-lookup"><span data-stu-id="4810a-131">Create Run As account from hello portal</span></span>
<span data-ttu-id="4810a-132">이 섹션에서는 다음 단계 tooupdate hello를 hello Azure 포털에서에서 Azure 자동화 계정을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-132">In this section, perform hello following steps tooupdate your Azure Automation account from  hello Azure portal.</span></span>  <span data-ttu-id="4810a-133">Hello 계정으로 실행 및 기존 실행 계정을 개별적으로 만들고 hello 클래식 Azure 포털에서 toomanage 리소스 필요가 없는 경우 hello Azure 실행 계정만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-133">You create hello Run As and Classic Run As accounts individually, and if you don't need toomanage resources in hello classic Azure portal, you can just create hello Azure Run As account.</span></span>  

<span data-ttu-id="4810a-134">hello 프로세스 hello 다음 자동화 계정에서 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-134">hello process creates hello following items in your Automation account.</span></span>

<span data-ttu-id="4810a-135">**실행 계정의 경우:**</span><span class="sxs-lookup"><span data-stu-id="4810a-135">**For Run As accounts:**</span></span>

* <span data-ttu-id="4810a-136">자체 서명 된 인증서로 Azure AD 응용 프로그램을 만듭니다, 그리고 hello 응용 프로그램에 대 한 서비스 주체 계정을 Azure AD에서 만들어지고 hello 계정 현재 구독에 대 한 hello 참가자 역할 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-136">Creates an Azure AD application with a self-signed certificate, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="4810a-137">이 설정은 tooOwner 또는 다른 역할을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-137">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="4810a-138">자세한 내용은 [Azure Automation의 역할 기반 액세스 제어](automation-role-based-access-control.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4810a-138">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="4810a-139">명명 된 자동화 인증서 자산을 만듭니다 *AzureRunAsCertificate* hello 자동화 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-139">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="4810a-140">hello 인증서 자산 hello Azure AD 응용 프로그램에서 사용 되는 hello 인증서 개인 키를 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-140">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="4810a-141">명명 된 자동화 연결 자산을 만듭니다 *AzureRunAsConnection* hello 자동화 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-141">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="4810a-142">hello applicationId, tenantId, subscriptionId, 및 인증서 지문을 hello 연결 자산을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-142">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="4810a-143">**클래식 실행 계정의 경우:**</span><span class="sxs-lookup"><span data-stu-id="4810a-143">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="4810a-144">명명 된 자동화 인증서 자산을 만듭니다 *AzureClassicRunAsCertificate* hello 자동화 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-144">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="4810a-145">hello 인증서 자산 hello 관리 인증서에 의해 사용 된 hello 인증서 개인 키를 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-145">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="4810a-146">명명 된 자동화 연결 자산을 만듭니다 *AzureClassicRunAsConnection* hello 자동화 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-146">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="4810a-147">hello 연결 자산 hello 구독 이름, subscriptionId, 이름과 인증서 자산을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-147">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

1. <span data-ttu-id="4810a-148">Hello 구독 관리자 역할의 멤버 및 hello 구독의 공동 관리자 인 계정으로 Azure 포털 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-148">Sign in toohello Azure portal with an account that is a member of hello Subscription Admins role and co-administrator of hello subscription.</span></span>
2. <span data-ttu-id="4810a-149">Hello 자동화 계정 블레이드에서 선택 **실행 계정** hello 섹션 아래의 **계정 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-149">From hello Automation account blade, select **Run As Accounts** under hello section **Account Settings**.</span></span>  
3. <span data-ttu-id="4810a-150">필요한 계정에 따라 **Azure 실행 계정** 또는 **Azure 클래식 실행 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-150">Depending on which account you require, select either **Azure Run As Account** or **Azure Classic Run As Account**.</span></span>  <span data-ttu-id="4810a-151">Hello 중 하나를 선택한 후 **추가 Azure 계정으로 실행** 또는 **Azure 클래식 실행 계정 추가** 블레이드 hello 개요 정보를 검토 한 후 클릭 나타나며 **만들기** 실행 계정 만들고와 tooproceed 합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-151">After selecting either hello **Add Azure Run As** or **Add Azure Classic Run As Account** blade appears and after reviewing hello overview information, click **Create** tooproceed with Run As account creation.</span></span>  
4. <span data-ttu-id="4810a-152">Azure hello 실행 계정을 만들고, 하지만 아래 hello 진행률을 추적할 수 있습니다 **알림** hello에서 메뉴와 배너 라는 메시지가 표시 됩니다 hello 계정을 만드는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-152">While Azure creates hello Run As account, you can track hello progress under **Notifications** from hello menu and a banner is displayed stating hello account is being created.</span></span>  <span data-ttu-id="4810a-153">이 프로세스는 몇 분 toocomplete를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-153">This process can take a few minutes toocomplete.</span></span>  

## <a name="create-run-as-account-using-powershell-script"></a><span data-ttu-id="4810a-154">PowerShell 스크립트를 사용하여 실행 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="4810a-154">Create Run As account using PowerShell script</span></span>
<span data-ttu-id="4810a-155">이 PowerShell 스크립트는 구성을 따르고 hello에 대 한 지원이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-155">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="4810a-156">자체 서명된 인증서를 사용하여 실행 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-156">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="4810a-157">자체 서명된 인증서를 사용하여 실행 계정 및 클래식 실행 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-157">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="4810a-158">엔터프라이즈 인증서를 사용하여 실행 계정 및 클래식 실행 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-158">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="4810a-159">Hello Azure Government 클라우드에서에서 자체 서명 된 인증서를 사용 하 여 실행 계정 및 기존 실행 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-159">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="4810a-160">선택한 hello 구성 옵션에 따라 hello 스크립트 hello 다음 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-160">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="4810a-161">**실행 계정의 경우:**</span><span class="sxs-lookup"><span data-stu-id="4810a-161">**For Run As accounts:**</span></span>

* <span data-ttu-id="4810a-162">만듭니다는 Azure AD 응용 프로그램 toobe 자체 서명 하거나 hello를 사용 하 여 내보낸 또는 엔터프라이즈 인증서 공개 키를 hello 응용 프로그램에 대 한 서비스 사용자 계정에 Azure AD를 만들고 할당 hello 후 현재에서 hello 계정에 대 한 참가자 역할 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-162">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="4810a-163">이 설정은 tooOwner 또는 다른 역할을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-163">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="4810a-164">자세한 내용은 [Azure Automation의 역할 기반 액세스 제어](automation-role-based-access-control.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4810a-164">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="4810a-165">명명 된 자동화 인증서 자산을 만듭니다 *AzureRunAsCertificate* hello 자동화 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-165">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="4810a-166">hello 인증서 자산 hello Azure AD 응용 프로그램에서 사용 되는 hello 인증서 개인 키를 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-166">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="4810a-167">명명 된 자동화 연결 자산을 만듭니다 *AzureRunAsConnection* hello 자동화 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-167">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="4810a-168">hello applicationId, tenantId, subscriptionId, 및 인증서 지문을 hello 연결 자산을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-168">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="4810a-169">**클래식 실행 계정의 경우:**</span><span class="sxs-lookup"><span data-stu-id="4810a-169">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="4810a-170">명명 된 자동화 인증서 자산을 만듭니다 *AzureClassicRunAsCertificate* hello 자동화 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-170">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="4810a-171">hello 인증서 자산 hello 관리 인증서에 의해 사용 된 hello 인증서 개인 키를 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-171">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="4810a-172">명명 된 자동화 연결 자산을 만듭니다 *AzureClassicRunAsConnection* hello 자동화 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-172">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="4810a-173">hello 연결 자산 hello 구독 이름, subscriptionId, 이름과 인증서 자산을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-173">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="4810a-174">Hello 스크립트를 실행 한 후 기본 계정으로 실행 계정 만들기에 대 한 옵션 중 하나를 선택 하면 업로드 hello 공용 인증서 (.cer 파일 이름 확장명) toohello 관리 저장 hello 구독에 대 한 해당 hello 자동화 계정에 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-174">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

1. <span data-ttu-id="4810a-175">컴퓨터에서 스크립트를 다음 hello를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-175">Save hello following script on your computer.</span></span> <span data-ttu-id="4810a-176">이 예제에서는 hello 파일 이름으로 저장 *새로 RunAsAccount.ps1*합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-176">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

        #Requires -RunAsAdministrator
        Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                       [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
            -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
            -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate = Get-Date $PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
            Sleep -s 10
            New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
            $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
            $Retries++;
        }
            return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 3 -and $AzureRMProfileVersion.Minor -ge 0) -or ($AzureRMProfileVersion.Major -gt 3)))
        {
            Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
            return
        }

        Login-AzureRmAccount -Environment $EnvironmentName 
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
           $CertificateName = $AutomationAccountName+$CertifcateAssetName
           $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
           $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
           $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
           CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
             # Create a Run As account by using a service principal
             $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
             $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
             $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
             $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                     "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                     "Then click Upload and upload hello .cer format of #CERT#"

              if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
              $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
              $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
              $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
              $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
              $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
              $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
              $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
              $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
              CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.Name
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="4810a-177">사용자 컴퓨터에서 시작 **Windows PowerShell** hello에서 **시작** 관리자 권한으로 화면입니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-177">On your computer, start **Windows PowerShell** from hello **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="4810a-178">Hello에서 높은 명령줄 셸 1 단계에서 만든 hello 스크립트가 들어 있는 이동 toohello 폴더.</span><span class="sxs-lookup"><span data-stu-id="4810a-178">From hello elevated command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>  
4. <span data-ttu-id="4810a-179">필요한 hello 구성에 대 한 hello 매개 변수 값을 사용 하 여 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-179">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="4810a-180">**자체 서명된 인증서를 사용하여 실행 계정 만들기**</span><span class="sxs-lookup"><span data-stu-id="4810a-180">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="4810a-181">**자체 서명된 인증서를 사용하여 실행 계정 및 클래식 실행 계정 만들기**</span><span class="sxs-lookup"><span data-stu-id="4810a-181">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="4810a-182">**엔터프라이즈 인증서를 사용하여 실행 계정 및 클래식 실행 계정 만들기**</span><span class="sxs-lookup"><span data-stu-id="4810a-182">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="4810a-183">**Hello Azure Government 클라우드에서에서 자체 서명 된 인증서를 사용 하 여 실행 계정 및 클래식 계정으로 실행 계정 만들기**</span><span class="sxs-lookup"><span data-stu-id="4810a-183">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="4810a-184">Hello 스크립트 실행 된 후 Azure 사용한 메시지 표시 tooauthenticate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-184">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="4810a-185">Hello 구독 관리자 역할의 구성원 및 hello 구독의 공동 관리자 인 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-185">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="4810a-186">Hello 스크립트 성공적으로 실행 된 후에 hello 다음 note:</span><span class="sxs-lookup"><span data-stu-id="4810a-186">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="4810a-187">Hello 스크립트 만들고 hello 사용자 프로필 아래에 임시 파일 폴더 toohello 저장 자체 서명 된 공용 인증서 (.cer 파일)를 사용 하 여 기존 실행 계정을 만든 경우 *%USERPROFILE%\AppData\Local\Temp*, tooexecute hello PowerShell 세션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-187">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="4810a-188">엔터프라이즈 공용 인증서(.cer 파일)를 사용하여 클래식 실행 계정을 만든 경우 이 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-188">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="4810a-189">에 대 한 hello 지침 [관리 API 인증서 toohello Azure 클래식 포털을 업로드](../azure-api-management-certs.md), hello를 사용 하 여 클래식 배포 리소스와 hello 자격 증명 구성의 유효성을 검사 하 [샘플 코드 Azure 클래식 배포 리소스와 tooauthenticate](automation-verify-runas-authentication.md#classic-run-as-authentication)합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-189">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with classic deployment resources by using hello [sample code tooauthenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="4810a-190">작업을 수행한 경우 *하지* 클래식 실행 계정을 만들고 리소스 관리자 리소스를 사용 하 여 인증 hello를 사용 하 여 hello 자격 증명 구성 유효성 검사 [서비스 관리를 사용 하 여 인증에 대 한 코드 샘플 리소스](automation-verify-runas-authentication.md#automation-run-as-authentication)합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-190">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4810a-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4810a-191">Next steps</span></span>
* <span data-ttu-id="4810a-192">서비스 사용자에 대 한 자세한 내용은 참조 너무[응용 프로그램 개체 및 서비스 주체 개체](../active-directory/active-directory-application-objects.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-192">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="4810a-193">인증서 및 Azure 서비스에 대 한 자세한 내용은 참조 너무[Azure 클라우드 서비스에 대 한 인증서 개요](../cloud-services/cloud-services-certs-create.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4810a-193">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
