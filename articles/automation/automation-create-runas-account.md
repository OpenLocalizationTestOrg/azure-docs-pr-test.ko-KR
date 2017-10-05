---
title: "Azure Automation 실행 계정 만들기 | Microsoft Docs"
description: "이 문서에서는 Automation 계정을 업데이트하고 PowerShell 또는 포털에서 실행 계정을 만드는 방법에 대해 설명합니다."
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
ms.openlocfilehash: eaf6eb49bbfe4572827fcc101d1f552b48ab91e6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="update-your-automation-account-authentication-with-run-as-accounts"></a><span data-ttu-id="2a98b-103">실행 계정으로 Automation 계정 인증 업데이트</span><span class="sxs-lookup"><span data-stu-id="2a98b-103">Update your Automation account authentication with Run As accounts</span></span> 
<span data-ttu-id="2a98b-104">다음과 같은 경우 포털 또는 PowerShell을 사용하여 기존 Automation 계정을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-104">You can update your existing Automation account from the portal or use PowerShell if:</span></span>

* <span data-ttu-id="2a98b-105">Automation 계정을 만들었지만 실행 계정 생성이 거부되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-105">You create an Automation account but decline to create the Run As account.</span></span>
* <span data-ttu-id="2a98b-106">Automation 계정을 이미 사용하여 Resource Manager 리소스를 관리하고 Runbook 인증을 위한 실행 계정을 포함하도록 계정을 업데이트하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-106">You already use an Automation account to manage Resource Manager resources and you want to update the account to include the Run As account for runbook authentication.</span></span>
* <span data-ttu-id="2a98b-107">Automation 계정을 사용하여 클래식 리소스를 관리하며 새 계정을 만들어서 Runbook 및 자산을 마이그레이션하는 대신 클래식 실행 계정을 사용하여 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-107">You already use an Automation account to manage classic resources and you want to update it to use the Classic Run As account instead of creating a new account and migrating your runbooks and assets to it.</span></span>   
* <span data-ttu-id="2a98b-108">엔터프라이즈 CA(인증 기관)에서 발급한 인증서를 사용하여 실행 및 클래식 실행 계정을 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-108">You want to create a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a98b-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2a98b-109">Prerequisites</span></span>

* <span data-ttu-id="2a98b-110">스크립트는 Azure Resource Manager 모듈 3.0.0 이상을 설치한 Windows 10 및 Windows Server 2016에서만 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-110">The script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 3.0.0 and later.</span></span> <span data-ttu-id="2a98b-111">이전 버전의 Windows에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="2a98b-112">Azure PowerShell 1.0 이상</span><span class="sxs-lookup"><span data-stu-id="2a98b-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="2a98b-113">PowerShell 1.0 릴리스에 대한 정보는 [Azure PowerShell 설치 및 구성 방법](/powershell/azureps-cmdlets-docs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a98b-113">For information about the PowerShell 1.0 release, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="2a98b-114">Automation 계정은 다음 PowerShell 스크립트에서 *–AutomationAccountName* 및 *-ApplicationDisplayName* 매개 변수의 값으로 참조됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-114">An Automation account, which is referenced as the value for the *–AutomationAccountName* and *-ApplicationDisplayName* parameters in the following PowerShell script.</span></span>

<span data-ttu-id="2a98b-115">스크립트의 필수 매개 변수인 *SubscriptionID*, *ResourceGroup* 및 *AutomationAccountName*의 값을 가져오려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-115">To get the values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for the script, do the following:</span></span>

1. <span data-ttu-id="2a98b-116">Azure Portal의 **Automation 계정** 블레이드에서 Automation 계정을 선택한 다음 **모든 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-116">In the Azure portal, select your Automation account on the **Automation account** blade, and then select **All settings**.</span></span>  
2. <span data-ttu-id="2a98b-117">**모든 설정** 블레이드의 **계정 설정** 아래에서 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-117">On the **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="2a98b-118">**속성** 블레이드에 대한 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-118">Note the values on the **Properties** blade.</span></span><br><br> <span data-ttu-id="2a98b-119">![Automation 계정 "속성" 블레이드](media/automation-create-runas-account/automation-account-properties.png)</span><span class="sxs-lookup"><span data-stu-id="2a98b-119">![The Automation account "Properties" blade](media/automation-create-runas-account/automation-account-properties.png)</span></span>  

### <a name="required-permissions-to-update-your-automation-account"></a><span data-ttu-id="2a98b-120">Automation 계정을 업데이트하는 데 필요한 권한</span><span class="sxs-lookup"><span data-stu-id="2a98b-120">Required permissions to update your Automation account</span></span>
<span data-ttu-id="2a98b-121">Automation 계정을 업데이트하려면 이 항목을 완료하는 데 필요한 다음과 같은 특정 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-121">To update an Automation account, you must have the following specific privileges and permissions required to complete this topic.</span></span>   
 
* <span data-ttu-id="2a98b-122">AD 사용자 계정은 [Azure Automation에서 역할 기반 액세스 제어](automation-role-based-access-control.md#contributor-role-permissions) 문서에 설명된 대로 Microsoft.Automation 리소스에 대한 참가자 역할과 동일한 권한을 가진 역할에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-122">Your AD user account needs to be added to a role with permissions equivalent to the Contributor role for Microsoft.Automation resources as outlined in article [Role-based access control in Azure Automation](automation-role-based-access-control.md#contributor-role-permissions).</span></span>  
* <span data-ttu-id="2a98b-123">Azure AD 테넌트의 관리자가 아닌 사용자는 앱 등록 설정이 **예**로 지정되어 있는 경우 [AD 응용 프로그램을 등록](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-123">Non-admin users in your Azure AD tenant can [register AD applications](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) if the App registrations setting is set to **Yes**.</span></span>  <span data-ttu-id="2a98b-124">앱 등록 설정이 **아니요**로 지정되어 있는 경우 이 작업을 수행하는 사용자는 Azure AD의 전역 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-124">If the app registrations setting is set to **No**, the user performing this action must be a global administrator in Azure AD.</span></span> 

<span data-ttu-id="2a98b-125">구독의 전역 관리자/공동 관리자 역할에 추가되기 전에 구독 Active Directory 인스턴스의 멤버가 아닌 경우 Active Directory에 게스트로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-125">If you are not a member of the subscription’s Active Directory instance before you are added to the global administrator/co-administrator role of the subscription, you are added to Active Directory as a guest.</span></span> <span data-ttu-id="2a98b-126">이 상황에서는 “만들 수 있는 사용 권한이 없습니다…”라는 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-126">In this situation, you receive a “You do not have permissions to create…”</span></span> <span data-ttu-id="2a98b-127">**Automation 계정 추가** 블레이드의 경고.</span><span class="sxs-lookup"><span data-stu-id="2a98b-127">warning on the **Add Automation Account** blade.</span></span> <span data-ttu-id="2a98b-128">전역 관리자/공동 관리자 역할에 처음 추가된 사용자는 구독 Active Directory 인스턴스에서 제거한 다음 다시 추가하여 Active Directory의 완전한 사용자로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-128">Users who were added to the global administrator/co-administrator role first can be removed from the subscription's Active Directory instance and re-added to make them a full User in Active Directory.</span></span> <span data-ttu-id="2a98b-129">Azure Portal의 **Azure Active Directory** 창에서 이 상황을 확인하려면 **사용자 및 그룹**을 선택한 다음 **모든 사용자**를 선택하거나 특정 사용자를 선택한 후 **프로필**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-129">To verify this situation, from the **Azure Active Directory** pane in the Azure portal, select **Users and groups**, select **All users** and, after you select the specific user, select **Profile**.</span></span> <span data-ttu-id="2a98b-130">사용자 프로필에서 **사용자 유형** 속성의 값은 **Guest**와 같지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-130">The value of the **User type** attribute under the users profile should not equal **Guest**.</span></span>

## <a name="create-run-as-account-from-the-portal"></a><span data-ttu-id="2a98b-131">포털에서 실행 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="2a98b-131">Create Run As account from the portal</span></span>
<span data-ttu-id="2a98b-132">이 섹션에서는 다음 단계를 수행하여 Azure Portal에서 Azure Automation 계정을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-132">In this section, perform the following steps to update your Azure Automation account from  the Azure portal.</span></span>  <span data-ttu-id="2a98b-133">실행 계정 및 클래식 실행 계정을 개별적으로 만들고, Azure 클래식 포털에서 리소스를 관리할 필요가 없는 경우 Azure 실행 계정을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-133">You create the Run As and Classic Run As accounts individually, and if you don't need to manage resources in the classic Azure portal, you can just create the Azure Run As account.</span></span>  

<span data-ttu-id="2a98b-134">이 프로세스에서 만드는 Automation 계정의 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-134">The process creates the following items in your Automation account.</span></span>

<span data-ttu-id="2a98b-135">**실행 계정의 경우:**</span><span class="sxs-lookup"><span data-stu-id="2a98b-135">**For Run As accounts:**</span></span>

* <span data-ttu-id="2a98b-136">자체 서명된 인증서로 Azure AD 응용 프로그램을 만들고, Azure AD에 응용 프로그램의 서비스 주체 계정을 만들며, 현재 구독에 있는 계정에 대해 참가자 역할을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-136">Creates an Azure AD application with a self-signed certificate, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="2a98b-137">이 설정을 소유자 또는 다른 어떤 역할로든 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-137">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="2a98b-138">자세한 내용은 [Azure Automation의 역할 기반 액세스 제어](automation-role-based-access-control.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a98b-138">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="2a98b-139">지정된 Automation 계정에서 *AzureRunAsCertificate*라는 Automation 인증서 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-139">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="2a98b-140">인증서 자산은 Azure AD 응용 프로그램에서 사용되는 인증서 개인 키를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-140">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="2a98b-141">지정된 Automation 계정에서 *AzureRunAsConnection*이라는 Automation 연결 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-141">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="2a98b-142">연결 자산은 applicationId, tenantId, subscriptionId 및 인증서 지문을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-142">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="2a98b-143">**클래식 실행 계정의 경우:**</span><span class="sxs-lookup"><span data-stu-id="2a98b-143">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="2a98b-144">지정된 Automation 계정에서 *AzureClassicRunAsCertificate*라는 Automation 인증서 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-144">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="2a98b-145">인증서 자산은 관리 인증서에서 사용되는 인증서 개인 키를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-145">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="2a98b-146">지정된 Automation 계정에서 *AzureClassicRunAsConnection*이라는 Automation 연결 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-146">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="2a98b-147">연결 자산은 구독 이름, subscriptionId 및 인증서 자산 이름을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-147">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

1. <span data-ttu-id="2a98b-148">구독 관리자 역할의 멤버이자 구독의 공동 관리자인 계정으로 Azure Portal에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-148">Sign in to the Azure portal with an account that is a member of the Subscription Admins role and co-administrator of the subscription.</span></span>
2. <span data-ttu-id="2a98b-149">Automation 계정 블레이드의 **계정 설정** 섹션 아래에서 **실행 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-149">From the Automation account blade, select **Run As Accounts** under the section **Account Settings**.</span></span>  
3. <span data-ttu-id="2a98b-150">필요한 계정에 따라 **Azure 실행 계정** 또는 **Azure 클래식 실행 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-150">Depending on which account you require, select either **Azure Run As Account** or **Azure Classic Run As Account**.</span></span>  <span data-ttu-id="2a98b-151">**Azure 실행 계정 추가** 또는 **Azure 클래식 실행 계정 추가** 블레이드 중 하나를 선택하여 해당 블레이드가 표시되면 개요 정보를 검토한 후에 **만들기**를 클릭하여 실행 계정 만들기 단계로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-151">After selecting either the **Add Azure Run As** or **Add Azure Classic Run As Account** blade appears and after reviewing the overview information, click **Create** to proceed with Run As account creation.</span></span>  
4. <span data-ttu-id="2a98b-152">Azure에서 실행 계정을 만드는 동안, 메뉴의 **알림**에서 진행률을 추적할 수 있으며 계정을 만들고 있음을 알리는 배너가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-152">While Azure creates the Run As account, you can track the progress under **Notifications** from the menu and a banner is displayed stating the account is being created.</span></span>  <span data-ttu-id="2a98b-153">이 프로세스를 완료하는 데 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-153">This process can take a few minutes to complete.</span></span>  

## <a name="create-run-as-account-using-powershell-script"></a><span data-ttu-id="2a98b-154">PowerShell 스크립트를 사용하여 실행 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="2a98b-154">Create Run As account using PowerShell script</span></span>
<span data-ttu-id="2a98b-155">이 PowerShell 스크립트는 다음 구성에 대한 지원을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-155">This PowerShell script includes support for the following configurations:</span></span>

* <span data-ttu-id="2a98b-156">자체 서명된 인증서를 사용하여 실행 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-156">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="2a98b-157">자체 서명된 인증서를 사용하여 실행 계정 및 클래식 실행 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-157">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="2a98b-158">엔터프라이즈 인증서를 사용하여 실행 계정 및 클래식 실행 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-158">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="2a98b-159">Azure Government 클라우드에서 자체 서명된 인증서를 사용하여 실행 계정 및 클래식 실행 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-159">Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud.</span></span>

<span data-ttu-id="2a98b-160">선택한 구성 옵션에 따라 스크립트는 다음 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-160">Depending on the configuration option you select, the script creates the following items.</span></span>

<span data-ttu-id="2a98b-161">**실행 계정의 경우:**</span><span class="sxs-lookup"><span data-stu-id="2a98b-161">**For Run As accounts:**</span></span>

* <span data-ttu-id="2a98b-162">자체 서명된 인증서 또는 엔터프라이즈 인증서 공개 키로 내보낼 Azure AD 응용 프로그램을 만들고, Azure AD에서 응용 프로그램의 서비스 주체 계정을 만들며, 현재 구독에서 이 계정의 참여자 역할을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-162">Creates an Azure AD application to be exported with either the self-signed or enterprise certificate public key, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="2a98b-163">이 설정을 소유자 또는 다른 어떤 역할로든 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-163">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="2a98b-164">자세한 내용은 [Azure Automation의 역할 기반 액세스 제어](automation-role-based-access-control.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a98b-164">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="2a98b-165">지정된 Automation 계정에서 *AzureRunAsCertificate*라는 Automation 인증서 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-165">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="2a98b-166">인증서 자산은 Azure AD 응용 프로그램에서 사용되는 인증서 개인 키를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-166">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="2a98b-167">지정된 Automation 계정에서 *AzureRunAsConnection*이라는 Automation 연결 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-167">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="2a98b-168">연결 자산은 applicationId, tenantId, subscriptionId 및 인증서 지문을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-168">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="2a98b-169">**클래식 실행 계정의 경우:**</span><span class="sxs-lookup"><span data-stu-id="2a98b-169">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="2a98b-170">지정된 Automation 계정에서 *AzureClassicRunAsCertificate*라는 Automation 인증서 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-170">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="2a98b-171">인증서 자산은 관리 인증서에서 사용되는 인증서 개인 키를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-171">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="2a98b-172">지정된 Automation 계정에서 *AzureClassicRunAsConnection*이라는 Automation 연결 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-172">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="2a98b-173">연결 자산은 구독 이름, subscriptionId 및 인증서 자산 이름을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-173">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="2a98b-174">클래식 실행 계정을 만드는 옵션을 선택한 경우 실행 스크립트를 실행한 후에 Automation 계정이 만들어진 구독의 관리 저장소에 공용 인증서(.cer 파일 이름 확장)를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-174">If you select either option for creating a Classic Run As account, after the script is executed, upload the public certificate (.cer file name extension) to the management store for the subscription that the Automation account was created in.</span></span>
> 

1. <span data-ttu-id="2a98b-175">컴퓨터에 다음 스크립트를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-175">Save the following script on your computer.</span></span> <span data-ttu-id="2a98b-176">이 예에서는 이를 *New-RunAsAccount.ps1*이라는 파일 이름으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-176">In this example, save it with the filename *New-RunAsAccount.ps1*.</span></span>

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

        # Sleep here for a few seconds to allow the service principal application to become active (ordinarily takes a few seconds)
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
            Write-Error -Message "Please install the latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
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

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate the ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
             # Create a Run As account by using a service principal
             $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
             $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
             $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
             $UploadMessage = "Please upload the .cer format of #CERT# to the Management store by following the steps below." + [Environment]::NewLine +
                     "Log in to the Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                     "Then click Upload and upload the .cer format of #CERT#"

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

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate the ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.Name
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="2a98b-177">사용자 컴퓨터의 **시작** 화면에서 관리자 권한으로 **Windows PowerShell**을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-177">On your computer, start **Windows PowerShell** from the **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="2a98b-178">승격된 명령줄 셸에서 1단계에서 만든 스크립트가 포함된 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-178">From the elevated command-line shell, go to the folder that contains the script you created in step 1.</span></span>  
4. <span data-ttu-id="2a98b-179">필요한 구성에 대한 매개 변수 값을 사용하여 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-179">Execute the script by using the parameter values for the configuration you require.</span></span>

    <span data-ttu-id="2a98b-180">**자체 서명된 인증서를 사용하여 실행 계정 만들기**</span><span class="sxs-lookup"><span data-stu-id="2a98b-180">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="2a98b-181">**자체 서명된 인증서를 사용하여 실행 계정 및 클래식 실행 계정 만들기**</span><span class="sxs-lookup"><span data-stu-id="2a98b-181">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="2a98b-182">**엔터프라이즈 인증서를 사용하여 실행 계정 및 클래식 실행 계정 만들기**</span><span class="sxs-lookup"><span data-stu-id="2a98b-182">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="2a98b-183">**Azure Government 클라우드에서 자체 서명된 인증서를 사용하여 실행 계정 및 클래식 실행 계정 만들기**</span><span class="sxs-lookup"><span data-stu-id="2a98b-183">**Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="2a98b-184">스크립트를 실행한 후에 Azure에 인증할지를 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-184">After the script has executed, you will be prompted to authenticate with Azure.</span></span> <span data-ttu-id="2a98b-185">구독 관리자 역할의 구성원이자 구독의 공동 관리자인 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-185">Sign in with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>
    >
    >

<span data-ttu-id="2a98b-186">스크립트가 성공적으로 실행된 후에 다음을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-186">After the script has executed successfully, note the following:</span></span>
* <span data-ttu-id="2a98b-187">자체 서명된 공용 인증서(.cer 파일)를 사용하여 클래식 실행 계정을 만든 경우 스크립트는 해당 계정을 만들고 PowerShell 세션을 실행하는 데 사용된 사용자 프로필(*%USERPROFILE%\AppData\Local\Temp*)의 컴퓨터에 있는 임시 파일 폴더에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-187">If you created a Classic Run As account with a self-signed public certificate (.cer file), the script creates and saves it to the temporary files folder on your computer under the user profile *%USERPROFILE%\AppData\Local\Temp*, which you used to execute the PowerShell session.</span></span>
* <span data-ttu-id="2a98b-188">엔터프라이즈 공용 인증서(.cer 파일)를 사용하여 클래식 실행 계정을 만든 경우 이 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-188">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="2a98b-189">[Azure 클래식 포털에 관리 API 인증서를 업로드](../azure-api-management-certs.md)하는 지침을 수행한 다음 [Azure 클래식 배포 리소스에서 인증하기 위한 샘플 코드](automation-verify-runas-authentication.md#classic-run-as-authentication)를 사용하여 클래식 배포 리소스에서 자격 증명 구성의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-189">Follow the instructions for [uploading a management API certificate to the Azure classic portal](../azure-api-management-certs.md), and then validate the credential configuration with classic deployment resources by using the [sample code to authenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="2a98b-190">클래식 실행 계정을 만들지 *않은* 경우 [Service Management 리소스에 인증하기 위한 샘플 코드](automation-verify-runas-authentication.md#automation-run-as-authentication)를 사용하여 Resource Manager 리소스에 인증하고 자격 증명 구성의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-190">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate the credential configuration by using the [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a98b-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2a98b-191">Next steps</span></span>
* <span data-ttu-id="2a98b-192">서비스 주체에 대한 자세한 내용은 [응용 프로그램 개체 및 서비스 주체 개체](../active-directory/active-directory-application-objects.md)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="2a98b-192">For more information about Service Principals, refer to [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="2a98b-193">인증서 및 Azure 서비스에 대한 자세한 내용은 [Azure Cloud Services 인증서 개요](../cloud-services/cloud-services-certs-create.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a98b-193">For more information about certificates and Azure services, refer to [Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>