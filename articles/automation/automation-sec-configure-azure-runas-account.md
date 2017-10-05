---
title: "Azure 실행 계정 구성 | Microsoft Docs"
description: "이 자습서는 Azure Automation에서 보안 주체 인증을 만들고 테스트하며 예제를 사용하는 과정을 설명합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
keywords: "서비스 주체 이름, setspn, azure 인증"
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/06/2017
ms.author: magoedte
ROBOTS: NOINDEX
redirect_url: /azure/automation/
redirect_document_id: TRUE
ms.openlocfilehash: f88c775eba19bb227d0e206d6420c08b57305b92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a><span data-ttu-id="82e83-104">Azure 실행 계정으로 Runbook 인증</span><span class="sxs-lookup"><span data-stu-id="82e83-104">Authenticate runbooks with an Azure Run As account</span></span>
<span data-ttu-id="82e83-105">이 문서에서는 Azure Portal에서 Azure Automation 계정을 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-105">This article shows you how to configure an Azure Automation account in the Azure portal.</span></span> <span data-ttu-id="82e83-106">이렇게 하려면 Azure Resource Manager 또는 Azure Service Management 중 하나에서 Runbook 관리 리소스를 인증하기 위해 실행 계정 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-106">To do so, you use the Run As account feature to authenticate runbooks managing resources in either Azure Resource Manager or Azure Service Management.</span></span>

<span data-ttu-id="82e83-107">Azure Portal에서 Automation 계정을 만들 경우 두 개의 계정을 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-107">When you create an Automation account in the Azure portal, you automatically create two accounts:</span></span>

* <span data-ttu-id="82e83-108">실행 계정</span><span class="sxs-lookup"><span data-stu-id="82e83-108">A Run As account.</span></span> <span data-ttu-id="82e83-109">이 계정은 Azure AD(Azure Active Directory)의 서비스 주체 및 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-109">This account creates a service principal in Azure Active Directory (Azure AD) and a certificate.</span></span> <span data-ttu-id="82e83-110">또한 Runbook을 사용하여 Resource Manager 리소스를 관리하는 참가자 역할 기반 액세스 제어(RBAC)를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-110">It also assigns the Contributor role-based access control (RBAC), which manages Resource Manager resources by using runbooks.</span></span>
* <span data-ttu-id="82e83-111">클래식 실행 계정</span><span class="sxs-lookup"><span data-stu-id="82e83-111">A Classic Run As account.</span></span> <span data-ttu-id="82e83-112">이 계정은 Runbook을 사용하여 Service Management 또는 클래식 리소스를 관리하는 데 사용되는 관리 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-112">This account uploads a management certificate, which is used to manage Service Management or classic resources by using runbooks.</span></span>

<span data-ttu-id="82e83-113">Automation 계정을 만들면 처리를 간편하게 만들고 자동화 요구를 지원하는 Runbook의 구축 및 배포를 신속하게 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-113">Creating an Automation account simplifies the process for you and helps you quickly start building and deploying runbooks to support your automation needs.</span></span>

<span data-ttu-id="82e83-114">실행 계정 및 클래식 실행 계정을 사용하여 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-114">With Run As and Classic Run As accounts, you can:</span></span>

* <span data-ttu-id="82e83-115">Azure Portal에서 Runbook의 Resource Manager 또는 Service Management 리소스를 관리하는 경우 Azure로 인증하는 표준화된 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-115">Provide a standardized way to authenticate with Azure when you manage Resource Manager or Service Management resources from runbooks in the Azure portal.</span></span>
* <span data-ttu-id="82e83-116">전역적인 Runbook의 사용을 자동화하면 Azure 경고에 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-116">Automate the use of global runbooks, which you can configure in Azure Alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="82e83-117">Automation 글로벌 Runbook을 포함한 [Azure 경고 통합 기능](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)에는 실행 계정 및 클래식 실행 계정이 구성된 Automation 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-117">The [Azure Alert integration feature](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) with Automation global runbooks requires an Automation account that's configured with a Run As account and a Classic Run As account.</span></span> <span data-ttu-id="82e83-118">실행 및 클래식 실행 계정을 이미 정의한 Automation 계정을 선택하거나 새로운 Automation 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-118">You can select an Automation account that already has defined Run As and Classic Run As accounts, or you can choose to create a new Automation account.</span></span>
>  

<span data-ttu-id="82e83-119">이 문서에서는 Azure Portal에서 Automation 계정을 만들고, Azure PowerShell을 사용하여 Automation 계정을 업데이트하고, 계정 구성을 관리하고, Runbook에서 인증하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-119">This article shows how to create an Automation account from the Azure portal, update an Automation account by using Azure PowerShell, manage the account configuration, and authenticate in your runbooks.</span></span>

<span data-ttu-id="82e83-120">Automation 계정을 만들기 전에 다음 항목을 이해하고 고려하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-120">Before you begin creating an Automation account, it's a good idea to understand and consider the following:</span></span>

* <span data-ttu-id="82e83-121">Automation 계정을 만드는 작업은 클래식 또는 Resource Manager 배포 모델에서 이미 만든 Automation 계정에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-121">Creating an Automation account does not affect Automation accounts you might have already created in either the classic or Resource Manager deployment model.</span></span>
* <span data-ttu-id="82e83-122">이 프로세스는 Azure Portal에서 만든 Automation 계정에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-122">The process works only for Automation accounts that you create in the Azure portal.</span></span> <span data-ttu-id="82e83-123">Azure 클래식 포털에서 계정을 만들려는 시도는 실행 계정 구성을 복제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-123">Attempting to create an account from the Azure classic portal does not replicate the Run As account configuration.</span></span>
* <span data-ttu-id="82e83-124">Runbook과 자산(예: 일정 또는 변수)을 배치하여 클래식 리소스를 관리하고 새 클래식 실행 계정을 사용하여 Runbook을 인증하려는 경우 다음 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-124">If you already have runbooks and assets (such as schedules or variables) in place to manage classic resources, and you want runbooks to authenticate with the new Classic Run As account, do either of the following:</span></span>

  * <span data-ttu-id="82e83-125">클래식 실행 계정을 만들려면 "관리 계정으로 실행" 섹션의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-125">To create a Classic Run As account, follow the instructions in the "Managing your Run As account" section.</span></span> 
  * <span data-ttu-id="82e83-126">기존 계정을 업데이트하려면 "PowerShell을 사용하여 Automation 계정 업데이트" 섹션에 있는 PowerShell 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-126">To update your existing account, use the PowerShell script in the "Update your Automation account by using PowerShell" section.</span></span>
* <span data-ttu-id="82e83-127">새 실행 계정 및 클래식 실행 Automation 계정을 사용하여 인증하려면 [인증 코드 예제](#authentication-code-examples) 섹션에서 제공된 예제 코드를 사용하여 기존 Runbook을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-127">To authenticate by using the new Run As account and Classic Run As Automation account, you  need to modify your existing runbooks with the example code provided in the section [Authentication code examples](#authentication-code-examples).</span></span>

    >[!NOTE]
    ><span data-ttu-id="82e83-128">실행 계정은 인증서 기반 서비스 주체를 사용하여 Resource Manager 리소스에 인증하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-128">The Run As account is for authentication against Resource Manager resources using the certificate-based service principal.</span></span> <span data-ttu-id="82e83-129">클래식 실행 계정은 관리 인증서를 사용하여 Service Management 리소스에 대해 인증하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-129">The Classic Run As account is for authenticating against Service Management resources with a management certificate.</span></span>

## <a name="create-an-automation-account-from-the-azure-portal"></a><span data-ttu-id="82e83-130">Azure Portal에서 Automation 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="82e83-130">Create an Automation account from the Azure portal</span></span>
<span data-ttu-id="82e83-131">이 섹션에서는 Azure Portal에서 Azure Automation 계정을 만듭니다. 그러면 실행 계정 및 클래식 실행 계정이 모두 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-131">In this section, you create an Azure Automation account from the Azure portal, which in turn creates both a Run As account and a Classic Run As account.</span></span>

>[!NOTE]
><span data-ttu-id="82e83-132">Automation 계정을 만들려면 서비스 관리자 역할의 구성원이거나 구독에 대한 액세스 권한을 부여하는 구독의 공동 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-132">To create an Automation account, you must be a member of the Service Admins role or co-administrator of the subscription that is granting access to the subscription.</span></span> <span data-ttu-id="82e83-133">또한 해당 구독의 기본 Active Directory 인스턴스에 사용자로 추가되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-133">You must also be added as a user to that subscription's default Active Directory instance.</span></span> <span data-ttu-id="82e83-134">이 계정은 권한 있는 역할에 할당할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-134">The account does not need to be assigned a privileged role.</span></span>
>
><span data-ttu-id="82e83-135">구독의 공동 관리자 역할에 추가되기 전에 구독 Active Directory 인스턴스의 구성원이 아닌 경우 Active Directory에 게스트로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-135">If you are not a member of the subscription’s Active Directory instance before you are added to the co-administrator role of the subscription, you will be added to Active Directory as a guest.</span></span> <span data-ttu-id="82e83-136">이 인스턴스에서는 “만들 수 있는 사용 권한이 없습니다…”라는 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-136">In this instance, you will receive a “You do not have permissions to create…”</span></span> <span data-ttu-id="82e83-137">**Automation 계정 추가** 블레이드의 경고.</span><span class="sxs-lookup"><span data-stu-id="82e83-137">warning on the **Add Automation Account** blade.</span></span>
>
><span data-ttu-id="82e83-138">공동 관리자 역할에 처음 추가된 사용자는 구독 Active Directory 인스턴스에서 제거한 다음 다시 추가하여 Active Directory의 완전한 사용자로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-138">Users who were added to the co-administrator role first can be removed from the subscription's Active Directory instance and re-added to make them a full User in Active Directory.</span></span> <span data-ttu-id="82e83-139">Azure Portal의 **Azure Active Directory** 창에서 이 상황을 확인하려면 **사용자 및 그룹**을 선택한 다음 **모든 사용자**를 선택하거나 특정 사용자를 선택한 후 **프로필**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-139">To verify this situation from the **Azure Active Directory** pane in the Azure portal by selecting **Users and groups**, selecting **All users** and, after you select the specific user, selecting **Profile**.</span></span> <span data-ttu-id="82e83-140">사용자 프로필에서 **사용자 유형** 속성의 값은 **Guest**와 같지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-140">The value of the **User type** attribute under the users profile should not equal **Guest**.</span></span>
>

1. <span data-ttu-id="82e83-141">구독 관리자 역할의 멤버이자 구독의 공동 관리자인 계정으로 Azure Portal에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-141">Sign in to the Azure portal with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>

2. <span data-ttu-id="82e83-142">**자동화 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-142">Select **Automation Accounts**.</span></span>

3. <span data-ttu-id="82e83-143">**Automation 계정** 블레이드에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-143">On the **Automation Accounts** blade, click **Add**.</span></span>
<span data-ttu-id="82e83-144">**Automation 계정 추가** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-144">The **Add Automation Account** blade opens.</span></span>

 !["Automation 계정 추가" 블레이드](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > <span data-ttu-id="82e83-146">사용자의 계정이 구독 관리자 역할의 구성원이자 구독의 공동 관리자가 아닌 경우 **Automation 계정 추가** 블레이드에서 다음과 같은 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-146">If your account is not a member of the subscription administrators role and co-administrator of the subscription, the following warning is displayed on the **Add Automation Account** blade:</span></span>
   >
   >![자동화 계정 경고 추가](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. <span data-ttu-id="82e83-148">**Automation 계정 추가** 블레이드의 **이름** 상자에 새 Automation 계정에 대한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-148">On the **Add Automation Account** blade, in the **Name** box, type a name for your new Automation account.</span></span>

5. <span data-ttu-id="82e83-149">구독이 두 개 이상인 경우 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-149">If you have more than one subscription, do the following:</span></span>

    <span data-ttu-id="82e83-150">a.</span><span class="sxs-lookup"><span data-stu-id="82e83-150">a.</span></span> <span data-ttu-id="82e83-151">**구독** 아래에서 새 계정의 구독을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-151">Under **Subscription**, specify one for the new account.</span></span>

    <span data-ttu-id="82e83-152">b.</span><span class="sxs-lookup"><span data-stu-id="82e83-152">b.</span></span> <span data-ttu-id="82e83-153">**리소스 그룹** 아래에서 **새로 만들기** 또는 **기존 항목 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-153">Under **Resource Group**, click **Create new** or **Use existing**.</span></span>

    <span data-ttu-id="82e83-154">c.</span><span class="sxs-lookup"><span data-stu-id="82e83-154">c.</span></span> <span data-ttu-id="82e83-155">**위치** 아래에서 Azure 데이터 센터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-155">Under **Location**, specify an Azure datacenter.</span></span>

6. <span data-ttu-id="82e83-156">**Azure 실행 계정 만들기** 아래에서 **예**를 선택하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-156">Under **Create Azure Run As account**, select **Yes**, and then click **Create**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="82e83-157">**아니요**를 선택하여 실행 계정을 만들지 않는 경우 **Automation 계정 추가** 블레이드에 경고 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-157">If you choose not to create the Run As account by selecting **No**, a warning message is displayed the **Add Automation Account** blade.</span></span> <span data-ttu-id="82e83-158">Azure Portal에서 계정이 생성되는 반면 클래식 또는 Resource Manager 구독 디렉터리 서비스 내에 해당하는 인증 ID가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-158">Although the account is created in the Azure portal, it does not have a corresponding authentication identity within your classic or Resource Manager subscription directory service.</span></span> <span data-ttu-id="82e83-159">따라서 계정에는 구독의 리소스에 대한 액세스 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-159">Consequently, the account has no access to resources in your subscription.</span></span> <span data-ttu-id="82e83-160">이 시나리오는 이 계정을 참조하는 Runbook이 그러한 배포 모델의 리소스에 대해 작업을 인증하고 수행하지 않도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-160">This scenario prevents any runbooks that reference this account from authenticating and performing tasks against resources in those deployment models.</span></span>
   >
   > !["Automation 계정 추가" 블레이드의 경고 메시지](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > <span data-ttu-id="82e83-162">또한 서비스 주체가 만들어지지 않은 경우 참여자 역할은 할당되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-162">Additionally, because the service principal is not created, the Contributor role is not assigned.</span></span>
   >

7. <span data-ttu-id="82e83-163">Azure에서 자동화 계정을 만드는 동안 메뉴의 **알림** 에서 진행률을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-163">While Azure creates the Automation account, you can track the progress under **Notifications** from the menu.</span></span>

### <a name="resources"></a><span data-ttu-id="82e83-164">리소스</span><span class="sxs-lookup"><span data-stu-id="82e83-164">Resources</span></span>
<span data-ttu-id="82e83-165">자동화 계정이 성공적으로 만들어지면 몇 가지 리소스가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-165">When the Automation account is successfully created, several resources are automatically created for you.</span></span> <span data-ttu-id="82e83-166">리소스는 다음과 같은 두 개의 테이블에 요약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-166">The resources are summarized in the following two tables:</span></span>

#### <a name="run-as-account-resources"></a><span data-ttu-id="82e83-167">실행 계정 리소스</span><span class="sxs-lookup"><span data-stu-id="82e83-167">Run As account resources</span></span>

| <span data-ttu-id="82e83-168">리소스</span><span class="sxs-lookup"><span data-stu-id="82e83-168">Resource</span></span> | <span data-ttu-id="82e83-169">설명</span><span class="sxs-lookup"><span data-stu-id="82e83-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="82e83-170">AzureAutomationTutorial Runbook</span><span class="sxs-lookup"><span data-stu-id="82e83-170">AzureAutomationTutorial Runbook</span></span> | <span data-ttu-id="82e83-171">실행 계정을 사용하여 인증하고 Resource Manager 리소스를 모두 가져오는 방법을 보여주는 예제 그래픽 Runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-171">An example graphical runbook that demonstrates how to authenticate by using the Run As account and gets all the Resource Manager resources.</span></span> |
| <span data-ttu-id="82e83-172">AzureAutomationTutorialScript Runbook</span><span class="sxs-lookup"><span data-stu-id="82e83-172">AzureAutomationTutorialScript Runbook</span></span> | <span data-ttu-id="82e83-173">실행 계정을 사용하여 인증하고 Resource Manager 리소스를 모두 가져오는 방법을 보여주는 예제 PowerShell Runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-173">An example PowerShell runbook that demonstrates how to authenticate by using the Run As account and gets all the Resource Manager resources.</span></span> |
| <span data-ttu-id="82e83-174">AzureRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="82e83-174">AzureRunAsCertificate</span></span> | <span data-ttu-id="82e83-175">Automation 계정을 만들거나 기존 계정에 대해 다음 PowerShell 스크립트를 사용하는 경우 자동으로 만들어지는 인증서 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-175">The certificate asset that's automatically created when you create an Automation account or use the following PowerShell script for an existing account.</span></span> <span data-ttu-id="82e83-176">인증서를 사용하면 Runbook에서 Azure Resource Manager 리소스를 관리할 수 있도록 Azure로 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-176">The certificate allows you to authenticate with Azure so that you can manage Azure Resource Manager resources from runbooks.</span></span> <span data-ttu-id="82e83-177">인증서의 수명은 1년입니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-177">The certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="82e83-178">AzureRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="82e83-178">AzureRunAsConnection</span></span> | <span data-ttu-id="82e83-179">Automation 계정을 만들거나 기존 계정에 대해 PowerShell 스크립트를 사용하는 경우 자동으로 만들어지는 연결 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-179">The connection asset that's automatically created when you create an Automation account or use the PowerShell script for an existing account.</span></span> |

#### <a name="classic-run-as-account-resources"></a><span data-ttu-id="82e83-180">클래식 실행 계정 리소스</span><span class="sxs-lookup"><span data-stu-id="82e83-180">Classic Run As account resources</span></span>

| <span data-ttu-id="82e83-181">리소스</span><span class="sxs-lookup"><span data-stu-id="82e83-181">Resource</span></span> | <span data-ttu-id="82e83-182">설명</span><span class="sxs-lookup"><span data-stu-id="82e83-182">Description</span></span> |
| --- | --- |
| <span data-ttu-id="82e83-183">AzureClassicAutomationTutorial Runbook</span><span class="sxs-lookup"><span data-stu-id="82e83-183">AzureClassicAutomationTutorial Runbook</span></span> | <span data-ttu-id="82e83-184">클래식 실행 계정(인증서)을 사용하여 구독의 모든 클래식 배포 모델을 사용하여 만든 VM을 가져온 다음 VM 이름 및 상태를 작성하는 예제 그래픽 Runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-184">An example graphical runbook that gets all the VMs that are created using the classic deployment model in a subscription by using the Classic Run As account (certificate), and then writes the VM name and status.</span></span> |
| <span data-ttu-id="82e83-185">AzureClassicAutomationTutorial Script Runbook</span><span class="sxs-lookup"><span data-stu-id="82e83-185">AzureClassicAutomationTutorial Script Runbook</span></span> | <span data-ttu-id="82e83-186">클래식 실행 계정(인증서)을 사용하여 구독의 모든 클래식 VM을 가져온 다음 VM 이름 및 상태를 작성하는 예제 PowerShell Runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-186">An example PowerShell runbook that gets all the classic VMs in a subscription by using the Classic Run As account (certificate), and then writes the VM name and status.</span></span> |
| <span data-ttu-id="82e83-187">AzureClassicRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="82e83-187">AzureClassicRunAsCertificate</span></span> | <span data-ttu-id="82e83-188">Runbook에서 Azure 클래식 리소스를 관리할 수 있도록 Azure에 인증하는 데 사용되는 자동으로 생성된 인증서 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-188">The automatically created certificate asset that you use to authenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> <span data-ttu-id="82e83-189">인증서의 수명은 1년입니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-189">The certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="82e83-190">AzureClassicRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="82e83-190">AzureClassicRunAsConnection</span></span> | <span data-ttu-id="82e83-191">Runbook에서 Azure 클래식 리소스를 관리할 수 있도록 Azure에 인증하는 데 사용되는 자동으로 생성된 연결 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-191">The automatically created connection asset that you use to authenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> |

## <a name="verify-run-as-authentication"></a><span data-ttu-id="82e83-192">실행 인증 확인</span><span class="sxs-lookup"><span data-stu-id="82e83-192">Verify Run As authentication</span></span>
<span data-ttu-id="82e83-193">작은 테스트를 수행하여 새 실행 계정을 사용하여 성공적으로 인증할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-193">Perform a small test to confirm that you can successfully authenticate by using the new Run As account.</span></span>

1. <span data-ttu-id="82e83-194">Azure 포털에서 이전에 만든 자동화 계정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-194">In the Azure portal, open the Automation account that you created earlier.</span></span>

2. <span data-ttu-id="82e83-195">**Runbook** 타일을 클릭하여 Runbook 목록을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-195">Click the **Runbooks** tile to open the list of runbooks.</span></span>

3. <span data-ttu-id="82e83-196">**AzureAutomationTutorialScript** Runbook을 선택한 다음 **시작**을 클릭하여 Runbook을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-196">Select the **AzureAutomationTutorialScript** runbook, and then click **Start** to start the runbook.</span></span> <span data-ttu-id="82e83-197">다음 이벤트가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-197">The following events occur:</span></span>
 * <span data-ttu-id="82e83-198">[Runbook 작업](automation-runbook-execution.md)이 만들어지고, **작업** 블레이드가 표시되며, **작업 요약** 타일에 작업 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-198">A [runbook job](automation-runbook-execution.md) is created, the **Job** blade is displayed, and the job status is displayed in the **Job Summary** tile.</span></span>
 * <span data-ttu-id="82e83-199">작업 상태는 클라우드의 Runbook worker를 사용할 수 있을 때까지 기다리고 있음을 나타내는 **대기 중**으로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-199">The job status begins as **Queued**, indicating that it is waiting for a runbook worker in the cloud to become available.</span></span>
 * <span data-ttu-id="82e83-200">작업자가 작업을 클레임하는 경우 상태는 **시작 중**이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-200">The status becomes **Starting** when a worker claims the job.</span></span>
 * <span data-ttu-id="82e83-201">Runbook이 실행되기 시작할 때 상태는 **실행 중**이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-201">The status becomes **Running** when the runbook starts running.</span></span>
 * <span data-ttu-id="82e83-202">Runbook 작업의 실행이 완료되면 **완료됨**이라는 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-202">When the runbook job has finished running, you should see a status of **Completed**.</span></span>

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. <span data-ttu-id="82e83-203">Runbook의 자세한 결과를 보려면 **출력** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-203">To see the detailed results of the runbook, click the **Output** tile.</span></span>  
<span data-ttu-id="82e83-204">**출력** 블레이드가 표시되고 Runbook이 리소스 그룹에서 사용할 수 있는 모든 리소스의 목록이 성공적으로 인증되고 반환되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-204">The **Output** blade is displayed, showing that the runbook has successfully authenticated and returned a list of all resources available in the resource group.</span></span>

5. <span data-ttu-id="82e83-205">**출력** 블레이드를 닫으면 **작업 요약** 블레이드로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-205">Close the **Output** blade to return to the **Job Summary** blade.</span></span>

6. <span data-ttu-id="82e83-206">**작업 요약** 블레이드 및 해당 **AzureAutomationTutorialScript** Runbook 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-206">Close the **Job Summary** blade and the corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="verify-classic-run-as-authentication"></a><span data-ttu-id="82e83-207">클래식 실행 인증 확인</span><span class="sxs-lookup"><span data-stu-id="82e83-207">Verify Classic Run As authentication</span></span>
<span data-ttu-id="82e83-208">새 클래식 실행 계정을 사용하여 성공적으로 인증될 수 있는지 확인하는 유사한 작은 테스트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-208">Perform a similar small test to confirm that you can successfully authenticate by using the new Classic Run As account.</span></span>

1. <span data-ttu-id="82e83-209">Azure 포털에서 이전에 만든 자동화 계정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-209">In the Azure portal, open the Automation account that you created earlier.</span></span>

2. <span data-ttu-id="82e83-210">**Runbook** 타일을 클릭하여 Runbook 목록을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-210">Click the **Runbooks** tile to open the list of runbooks.</span></span>

3. <span data-ttu-id="82e83-211">**AzureClassicAutomationTutorialScript** Runbook을 선택한 다음 **시작**을 클릭하여 Runbook을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-211">Select the **AzureClassicAutomationTutorialScript** runbook, and then click **Start** to  start the runbook.</span></span> <span data-ttu-id="82e83-212">다음 이벤트가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-212">The following events occur:</span></span>

 * <span data-ttu-id="82e83-213">[Runbook 작업](automation-runbook-execution.md)이 만들어지고, **작업** 블레이드가 표시되며, **작업 요약** 타일에 작업 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-213">A [runbook job](automation-runbook-execution.md) is created, the **Job** blade is displayed, and the job status is displayed in the **Job Summary** tile.</span></span>
 * <span data-ttu-id="82e83-214">작업 상태는 클라우드의 Runbook worker를 사용할 수 있을 때까지 기다리고 있음을 나타내는 **대기 중**으로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-214">The job status begins as **Queued**, indicating that it is waiting for a runbook worker in the cloud to become available.</span></span>
 * <span data-ttu-id="82e83-215">작업자가 작업을 클레임하는 경우 상태는 **시작 중**이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-215">The status becomes **Starting** when a worker claims the job.</span></span>
 * <span data-ttu-id="82e83-216">Runbook이 실행되기 시작할 때 상태는 **실행 중**이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-216">The status becomes **Running** when the runbook starts running.</span></span>
 * <span data-ttu-id="82e83-217">Runbook 작업의 실행이 완료되면 **완료됨**이라는 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-217">When the runbook job has finished running, you should see a status of **Completed**.</span></span>

    ![보안 주체 Runbook 테스트](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. <span data-ttu-id="82e83-219">Runbook의 자세한 결과를 보려면 **출력** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-219">To see the detailed results of the runbook, click the **Output** tile.</span></span>  
<span data-ttu-id="82e83-220">**출력** 블레이드가 표시되고 Runbook이 구독에서 모든 클래식 VM 목록을 성공적으로 인증하고 반환한 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-220">The **Output** blade is displayed, showing that the runbook has successfully authenticated and returned a list of all classic VMs in the subscription.</span></span>

5. <span data-ttu-id="82e83-221">**출력** 블레이드를 닫으면 **작업 요약** 블레이드로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-221">Close the **Output** blade to return to the **Job Summary** blade.</span></span>

6. <span data-ttu-id="82e83-222">**작업 요약** 블레이드 및 해당 **AzureAutomationTutorialScript** Runbook 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-222">Close the **Job Summary** blade and the corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="managing-your-run-as-account"></a><span data-ttu-id="82e83-223">Azure 실행 계정 관리</span><span class="sxs-lookup"><span data-stu-id="82e83-223">Managing your Run As account</span></span>
<span data-ttu-id="82e83-224">Automation 계정 만료되기 전인 어떤 시점에서 인증서를 갱신해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-224">At some point before your Automation account expires, you will need to renew the certificate.</span></span> <span data-ttu-id="82e83-225">실행 계정이 손상되었다고 생각하시면 삭제하고 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-225">If you believe that the Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="82e83-226">이 섹션에서는 이러한 작업을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-226">This section discusses how to perform these operations.</span></span>

### <a name="self-signed-certificate-renewal"></a><span data-ttu-id="82e83-227">자체 서명된 인증서 갱신</span><span class="sxs-lookup"><span data-stu-id="82e83-227">Self-signed certificate renewal</span></span>
<span data-ttu-id="82e83-228">실행 계정에 만든 자체 서명된 인증서는 생성 날짜로부터 1년이 되는 날에 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-228">The self-signed certificate that you created for the Run As account expires one year from the date of creation.</span></span> <span data-ttu-id="82e83-229">만료되기 전에 언제든지 갱신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-229">You can renew it at any time before it expires.</span></span> <span data-ttu-id="82e83-230">인증서를 갱신하면 큐에 대기하거나 활발하게 실행 중이며 실행 계정으로 인증되는 모든 Runbook이 부정적인 영향을 받지 않도록 현재 유효한 인증서가 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-230">When you renew it, the current valid certificate is retained to ensure that any runbooks that are queued up or actively running, and that authenticate with the Run As account, are not negatively affected.</span></span> <span data-ttu-id="82e83-231">인증서는 만료 날짜까지 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-231">The certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="82e83-232">엔터프라이즈 인증 기관에서 발급한 인증서를 사용하도록 Automation 실행 계정을 구성하고 이 옵션을 사용하는 경우 엔터프라이즈 인증서는 자체 서명된 인증서로 교체됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-232">If you have configured your Automation Run As account to use a certificate issued by your enterprise certificate authority and you use this option, the enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="82e83-233">인증서를 갱신하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-233">To renew the certificate, do the following:</span></span>

1. <span data-ttu-id="82e83-234">Azure Portal에서 Automation 계정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-234">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="82e83-235">**Automation 계정** 블레이드의 **계정 속성** 창에서 **계정 설정** 섹션 아래에 있는 **실행 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-235">On the **Automation Account** blade, in the **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Automation 계정 속성 창](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. <span data-ttu-id="82e83-237">**실행 계정** 속성 블레이드에서 인증서를 갱신하려는 실행 계정 또는 클래식 실행 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-237">On the **Run As Accounts** properties blade, select either the Run As account or the Classic Run As account that you want to renew the certificate for.</span></span>

4. <span data-ttu-id="82e83-238">선택한 계정의 **속성** 블레이드에서 **인증서 갱신**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-238">On the **Properties** blade for the selected account, click **Renew certificate**.</span></span>

    ![실행 계정용 인증서 갱신](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="82e83-240">인증서가 갱신되는 동안 메뉴의 **알림**에서 진행률을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-240">While the certificate is being renewed, you can track the progress under **Notifications** from the menu.</span></span>

### <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="82e83-241">실행 또는 클래식 실행 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="82e83-241">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="82e83-242">이 섹션에서는 실행 또는 클래식 실행 계정을 삭제하고 다시 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-242">This section describes how to delete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="82e83-243">이 작업을 실행하는 경우 Automation 계정이 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-243">When you perform this action, the Automation account is retained.</span></span> <span data-ttu-id="82e83-244">실행 또는 클래식 실행 계정을 삭제한 후에 Azure Portal에서 계정을 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-244">After you delete a Run As or Classic Run As account, you can re-create it in the Azure portal.</span></span>

1. <span data-ttu-id="82e83-245">Azure Portal에서 Automation 계정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-245">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="82e83-246">**Automation 계정** 블레이드의 계정 속성 창에서 **실행 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-246">On the **Automation account** blade, in the account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="82e83-247">**실행 계정** 속성 블레이드에서 삭제하려는 실행 계정 또는 클래식 실행 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-247">On the **Run As Accounts** properties blade, select either the Run As account or Classic Run As account that you want to delete.</span></span> <span data-ttu-id="82e83-248">그런 다음 선택한 계정의 **속성** 블레이드에서 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-248">Then, on the **Properties** blade for the selected account, click **Delete**.</span></span>

 ![실행 계정 삭제](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. <span data-ttu-id="82e83-250">계정이 삭제되는 동안 메뉴의 **알림** 에서 진행률을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-250">While the account is being deleted, you can track the progress under **Notifications** from the menu.</span></span>

5. <span data-ttu-id="82e83-251">계정이 삭제되면 **실행 계정** 속성 블레이드에서 **Azure 실행 계정** 만들기 옵션을 선택하여 계정을 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-251">After the account has been deleted, you can re-create it on the **Run As Accounts** properties blade by selecting the create option **Azure Run As Account**.</span></span>

 ![Automation 실행 계정 다시 만들기](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a><span data-ttu-id="82e83-253">잘못된 구성</span><span class="sxs-lookup"><span data-stu-id="82e83-253">Misconfiguration</span></span>
<span data-ttu-id="82e83-254">실행 또는 클래식 실행 계정이 제대로 작동하는 데 필요한 일부 구성 항목이 초기 설정 중에 제대로 삭제되거나 생성되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-254">Some configuration items necessary for the Run As or Classic Run As account to function properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="82e83-255">항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-255">The items include:</span></span>

* <span data-ttu-id="82e83-256">인증서 자산</span><span class="sxs-lookup"><span data-stu-id="82e83-256">Certificate asset</span></span>
* <span data-ttu-id="82e83-257">연결 자산</span><span class="sxs-lookup"><span data-stu-id="82e83-257">Connection asset</span></span>
* <span data-ttu-id="82e83-258">실행 계정이 참여자 역할에서 제거됨</span><span class="sxs-lookup"><span data-stu-id="82e83-258">Run As account has been removed from the contributor role</span></span>
* <span data-ttu-id="82e83-259">Azure AD의 서비스 주체 또는 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="82e83-259">Service principal or application in Azure AD</span></span>

<span data-ttu-id="82e83-260">잘못된 구성의 이전 및 다른 인스턴스에서 Automation 계정은 변경 사항을 감지하고 계정의 **실행 계정** 속성 블레이드에서 *불완전*이라는 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-260">In the preceding and other instances of misconfiguration, the Automation account detects the changes and displays a status of *Incomplete* on the **Run As Accounts** properties blade for the account.</span></span>

![불완전 실행 계정 구성 상태](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="82e83-262">실행 계정을 선택하면 계정 **속성** 창은 다음과 같은 오류 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-262">When you select the Run As account, the account **Properties** pane displays the following error message:</span></span>

![불완전 실행 계정 구성 경고 메시지](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="82e83-264">등 4가지 유형의 클러스터가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-264">.</span></span>

<span data-ttu-id="82e83-265">계정을 삭제하고 다시 만들어서 이러한 실행 계정 문제를 신속하게 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-265">You can quickly resolve these Run As account issues by deleting and re-creating the account.</span></span>

## <a name="update-your-automation-account-by-using-powershell"></a><span data-ttu-id="82e83-266">PowerShell을 사용하여 Automation 계정 업데이트</span><span class="sxs-lookup"><span data-stu-id="82e83-266">Update your Automation account by using PowerShell</span></span>
<span data-ttu-id="82e83-267">다음과 같은 경우 기존 Automation 계정을 업데이트하기 위해 PowerShell을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-267">You can use PowerShell to update your existing Automation account if:</span></span>

* <span data-ttu-id="82e83-268">Automation 계정을 만들었지만 실행 계정 생성이 거부되었습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-268">You create an Automation account but decline to create the Run As account.</span></span>
* <span data-ttu-id="82e83-269">Automation 계정을 이미 사용하여 Resource Manager 리소스를 관리하고 Runbook 인증을 위한 실행 계정을 포함하도록 계정을 업데이트하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-269">You already use an Automation account to manage Resource Manager resources and you want to update the account to include the Run As account for runbook authentication.</span></span>
* <span data-ttu-id="82e83-270">Automation 계정을 사용하여 클래식 리소스를 관리하며 새 계정을 만들어서 Runbook 및 자산을 마이그레이션하는 대신 클래식 실행 계정을 사용하여 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-270">You already use an Automation account to manage classic resources and you want to update it to use the Classic Run As account instead of creating a new account and migrating your runbooks and assets to it.</span></span>   
* <span data-ttu-id="82e83-271">엔터프라이즈 CA(인증 기관)에서 발급한 인증서를 사용하여 실행 및 클래식 실행 계정을 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-271">You want to create a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

<span data-ttu-id="82e83-272">스크립트에는 다음과 같은 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-272">The script has the following prerequisites:</span></span>

* <span data-ttu-id="82e83-273">스크립트는 Azure Resource Manager 모듈 2.01 이상이 설치되어 있는 Windows 10 및Windows Server 2016에서만 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-273">The script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="82e83-274">이전 버전의 Windows에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-274">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="82e83-275">Azure PowerShell 1.0 이상</span><span class="sxs-lookup"><span data-stu-id="82e83-275">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="82e83-276">PowerShell 1.0 릴리스에 대한 정보는 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82e83-276">For information about the PowerShell 1.0 release, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="82e83-277">Automation 계정은 다음 PowerShell 스크립트에서 *–AutomationAccountName* 및 *-ApplicationDisplayName* 매개 변수의 값으로 참조됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-277">An Automation account, which is referenced as the value for the *–AutomationAccountName* and *-ApplicationDisplayName* parameters in the following PowerShell script.</span></span>

<span data-ttu-id="82e83-278">스크립트의 필수 매개 변수인 *SubscriptionID*, *ResourceGroup* 및 *AutomationAccountName*의 값을 가져오려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-278">To get the values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for the scripts, do the following:</span></span>
1. <span data-ttu-id="82e83-279">Azure Portal의 **Automation 계정** 블레이드에서 Automation 계정을 선택한 다음 **모든 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-279">In the Azure portal, select your Automation account on the **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="82e83-280">**모든 설정** 블레이드의 **계정 설정** 아래에서 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-280">On the **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="82e83-281">**속성** 블레이드에 대한 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-281">Note the values on the **Properties** blade.</span></span>

![Automation 계정 "속성" 블레이드](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a><span data-ttu-id="82e83-283">실행 계정 PowerShell 스크립트 만들기</span><span class="sxs-lookup"><span data-stu-id="82e83-283">Create a Run As account PowerShell script</span></span>
<span data-ttu-id="82e83-284">이 PowerShell 스크립트는 다음 구성에 대한 지원을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-284">This PowerShell script includes support for the following configurations:</span></span>

* <span data-ttu-id="82e83-285">자체 서명된 인증서를 사용하여 실행 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-285">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="82e83-286">자체 서명된 인증서를 사용하여 실행 계정 및 클래식 실행 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-286">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="82e83-287">엔터프라이즈 인증서를 사용하여 실행 계정 및 클래식 실행 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-287">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="82e83-288">Azure Government 클라우드에서 자체 서명된 인증서를 사용하여 실행 계정 및 클래식 실행 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-288">Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud.</span></span>

<span data-ttu-id="82e83-289">선택한 구성 옵션에 따라 스크립트는 다음 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-289">Depending on the configuration option you select, the script creates the following items.</span></span>

<span data-ttu-id="82e83-290">**실행 계정의 경우:**</span><span class="sxs-lookup"><span data-stu-id="82e83-290">**For Run As accounts:**</span></span>

* <span data-ttu-id="82e83-291">자체 서명된 인증서 또는 엔터프라이즈 인증서 공개 키로 내보낼 Azure AD 응용 프로그램을 만들고, Azure AD에서 응용 프로그램의 서비스 주체 계정을 만들며, 현재 구독에서 이 계정의 참여자 역할을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-291">Creates an Azure AD application to be exported with either the self-signed or enterprise certificate public key, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="82e83-292">이 설정을 소유자 또는 다른 어떤 역할로든 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-292">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="82e83-293">자세한 내용은 [Azure Automation의 역할 기반 액세스 제어](automation-role-based-access-control.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82e83-293">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="82e83-294">지정된 Automation 계정에서 *AzureRunAsCertificate*라는 Automation 인증서 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-294">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="82e83-295">인증서 자산은 Azure AD 응용 프로그램에서 사용되는 인증서 개인 키를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-295">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="82e83-296">지정된 Automation 계정에서 *AzureRunAsConnection*이라는 Automation 연결 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-296">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="82e83-297">연결 자산은 applicationId, tenantId, subscriptionId 및 인증서 지문을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-297">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="82e83-298">**클래식 실행 계정의 경우:**</span><span class="sxs-lookup"><span data-stu-id="82e83-298">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="82e83-299">지정된 Automation 계정에서 *AzureClassicRunAsCertificate*라는 Automation 인증서 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-299">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="82e83-300">인증서 자산은 관리 인증서에서 사용되는 인증서 개인 키를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-300">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="82e83-301">지정된 Automation 계정에서 *AzureClassicRunAsConnection*이라는 Automation 연결 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-301">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="82e83-302">연결 자산은 구독 이름, subscriptionId 및 인증서 자산 이름을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-302">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="82e83-303">클래식 실행 계정을 만드는 옵션을 선택한 경우 실행 스크립트를 실행한 후에 Automation 계정이 만들어진 구독의 관리 저장소에 공용 인증서(.cer 파일 이름 확장)를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-303">If you select either option for creating a Classic Run As account, after the script is executed, upload the public certificate (.cer file name extension) to the management store for the subscription that the Automation account was created in.</span></span>
> 

<span data-ttu-id="82e83-304">스크립트를 실행하고 인증서를 업로드하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-304">To execute the script and upload the certificate, do the following:</span></span>

1. <span data-ttu-id="82e83-305">컴퓨터에 다음 스크립트를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-305">Save the following script on your computer.</span></span> <span data-ttu-id="82e83-306">이 예에서는 이를 *New-RunAsAccount.ps1*이라는 파일 이름으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-306">In this example, save it with the filename *New-RunAsAccount.ps1*.</span></span>

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
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
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
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install the latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
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
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="82e83-307">사용자 컴퓨터에서 **시작**을 클릭한 다음 관리자 권한으로**Windows PowerShell**을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-307">On your computer, click **Start**, and then start **Windows PowerShell** with elevated user rights.</span></span>

3. <span data-ttu-id="82e83-308">승격된 PowerShell 명령줄 셸에서 1단계에서 만든 스크립트가 포함된 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-308">From the elevated PowerShell command-line shell, go to the folder that contains the script you created in step 1.</span></span>

4. <span data-ttu-id="82e83-309">필요한 구성에 대한 매개 변수 값을 사용하여 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-309">Execute the script by using the parameter values for the configuration you require.</span></span>

    <span data-ttu-id="82e83-310">**자체 서명된 인증서를 사용하여 실행 계정 만들기**</span><span class="sxs-lookup"><span data-stu-id="82e83-310">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="82e83-311">**자체 서명된 인증서를 사용하여 실행 계정 및 클래식 실행 계정 만들기**</span><span class="sxs-lookup"><span data-stu-id="82e83-311">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="82e83-312">**엔터프라이즈 인증서를 사용하여 실행 계정 및 클래식 실행 계정 만들기**</span><span class="sxs-lookup"><span data-stu-id="82e83-312">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="82e83-313">**Azure Government 클라우드에서 자체 서명된 인증서를 사용하여 실행 계정 및 클래식 실행 계정 만들기**</span><span class="sxs-lookup"><span data-stu-id="82e83-313">**Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="82e83-314">스크립트를 실행한 후에 Azure에 인증할지를 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-314">After the script has executed, you will be prompted to authenticate with Azure.</span></span> <span data-ttu-id="82e83-315">구독 관리자 역할의 구성원이자 구독의 공동 관리자인 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-315">Sign in with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>
    >
    >

<span data-ttu-id="82e83-316">스크립트가 성공적으로 실행된 후에 다음을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-316">After the script has executed successfully, note the following:</span></span>
* <span data-ttu-id="82e83-317">자체 서명된 공용 인증서(.cer 파일)를 사용하여 클래식 실행 계정을 만든 경우 스크립트는 해당 계정을 만들고 PowerShell 세션을 실행하는 데 사용된 사용자 프로필(*%USERPROFILE%\AppData\Local\Temp*)의 컴퓨터에 있는 임시 파일 폴더에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-317">If you created a Classic Run As account with a self-signed public certificate (.cer file), the script creates and saves it to the temporary files folder on your computer under the user profile *%USERPROFILE%\AppData\Local\Temp*, which you used to execute the PowerShell session.</span></span>
* <span data-ttu-id="82e83-318">엔터프라이즈 공용 인증서(.cer 파일)를 사용하여 클래식 실행 계정을 만든 경우 이 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-318">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="82e83-319">[Azure 클래식 포털에 관리 API 인증서를 업로드](../azure-api-management-certs.md)하는 지침을 수행한 다음 [Service Management 리소스에 인증하기 위한 샘플 코드](#sample-code-to-authenticate-with-service-management-resources)를 사용하여 Service Management 리소스에서 자격 증명 구성의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-319">Follow the instructions for [uploading a management API certificate to the Azure classic portal](../azure-api-management-certs.md), and then validate the credential configuration with Service Management resources by using the [sample code to authenticate with Service Management Resources](#sample-code-to-authenticate-with-service-management-resources).</span></span> 
* <span data-ttu-id="82e83-320">클래식 실행 계정을 만들지 *않은* 경우 [Service Management 리소스에 인증하기 위한 샘플 코드](#sample-code-to-authenticate-with-resource-manager-resources)를 사용하여 Resource Manager 리소스에 인증하고 자격 증명 구성의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-320">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate the credential configuration by using the [sample code for authenticating with Service Management resources](#sample-code-to-authenticate-with-resource-manager-resources).</span></span>

## <a name="sample-code-to-authenticate-with-resource-manager-resources"></a><span data-ttu-id="82e83-321">Resource Manager 리소스를 사용하여 인증하는 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="82e83-321">Sample code to authenticate with Resource Manager resources</span></span>
<span data-ttu-id="82e83-322">Runbook으로 Resource Manager 리소스를 관리하는 실행 계정을 사용하여 인증하기 위해 *AzureAutomationTutorialScript* 예제 Runbook에서 가져온 다음의 업데이트된 샘플 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-322">You can use the following updated sample code, taken from the *AzureAutomationTutorialScript* example runbook, to authenticate by using the Run As account to manage Resource Manager resources with your runbooks.</span></span>

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get the connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in to Azure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context to a specific subscription"     
       Set-AzureRmContext -SubscriptionId $SubId              
    }
    catch {
        if (!$servicePrincipalConnection)
        {
           $ErrorMessage = "Connection $connectionName not found."
           throw $ErrorMessage
         } else{
            Write-Error -Message $_.Exception
            throw $_.Exception
         }
    }

<span data-ttu-id="82e83-323">여러 구독 간에 쉽게 작업할 수 있도록 스크립트에는 구독 컨텍스트를 참조하기 위해 지원되는 두 개의 코드 줄이 추가로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-323">To help you to easily work between multiple subscriptions, the script includes two additional lines of code that support referencing a subscription context.</span></span> <span data-ttu-id="82e83-324">*SubscriptionId*라는 변수 자산에는 구독의 ID가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-324">A variable asset named *SubscriptionId* contains the ID of the subscription.</span></span> <span data-ttu-id="82e83-325">`Add-AzureRmAccount` cmdlet 문 다음에 [`Set-AzureRmContext`](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet은 매개 변수 집합 *-SubscriptionId*로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-325">After the `Add-AzureRmAccount` cmdlet statement, the [`Set-AzureRmContext`](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet is stated with the parameter set *-SubscriptionId*.</span></span> <span data-ttu-id="82e83-326">변수 이름이 너무 일반적인 경우 식별하기 쉽도록 수정하여 접두사를 포함하거나 다른 명명 규칙을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-326">If the variable name is too generic, you can revise it to include a prefix or use another naming convention to make it easier to identify.</span></span> <span data-ttu-id="82e83-327">또한 해당하는 변수 자산이 있는 *-SubscriptionId* 대신 *-SubscriptionName* 매개 변수 집합을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-327">Alternatively, you can use the parameter set *-SubscriptionName* instead of *-SubscriptionId* with a corresponding variable asset.</span></span>

<span data-ttu-id="82e83-328">Runbook `Add-AzureRmAccount`에서 인증에 사용되는 cmdlet은 *ServicePrincipalCertificate* 매개 변수 집합을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-328">The cmdlet that you use for authenticating in the runbook, `Add-AzureRmAccount`, uses the *ServicePrincipalCertificate* parameter set.</span></span> <span data-ttu-id="82e83-329">사용자 자격 증명이 아니라 서비스 주체 인증서를 사용하여 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-329">It authenticates by using the service principal certificate, not the user credentials.</span></span>

## <a name="sample-code-to-authenticate-with-service-management-resources"></a><span data-ttu-id="82e83-330">Service Management 리소스를 사용하여 인증하는 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="82e83-330">Sample code to authenticate with Service Management resources</span></span>
<span data-ttu-id="82e83-331">Runbook으로 클래식 리소스를 관리하는 클래식 실행 계정을 사용하여 인증하기 위해 *AzureClassicAutomationTutorialScript* 예제 Runbook에서 가져온 다음의 업데이트된 샘플 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e83-331">You can use the following updated sample code, which is taken from the *AzureClassicAutomationTutorialScript* example runbook, to authenticate by using the Classic Run As account to manage classic resources with your runbooks.</span></span>

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get the connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate to Azure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in the Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting the certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in the Automation account."
    }

    Write-Verbose "Authenticating to Azure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a><span data-ttu-id="82e83-332">다음 단계</span><span class="sxs-lookup"><span data-stu-id="82e83-332">Next steps</span></span>
* [<span data-ttu-id="82e83-333">Azure AD의 응용 프로그램 및 서비스 주체 개체</span><span class="sxs-lookup"><span data-stu-id="82e83-333">Application and service principal objects in Azure AD</span></span>](../active-directory/active-directory-application-objects.md)
* [<span data-ttu-id="82e83-334">Azure Automation의 역할 기반 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="82e83-334">Role-based access control in Azure Automation</span></span>](automation-role-based-access-control.md)
* [<span data-ttu-id="82e83-335">Azure Cloud Services의 인증서 개요</span><span class="sxs-lookup"><span data-stu-id="82e83-335">Certificates overview for Azure Cloud Services</span></span>](../cloud-services/cloud-services-certs-create.md)
