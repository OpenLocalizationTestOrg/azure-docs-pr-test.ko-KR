---
title: "Azure Automation 계정 관리 | Microsoft Docs"
description: "이 문서에서는 인증서 갱신, 삭제 및 잘못된 구성과 같은 Automation 계정의 구성을 관리하는 방법을 설명합니다."
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
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 41efdbcacede74bac038342688362ff480cadc7e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-automation-account"></a><span data-ttu-id="4fcfe-103">Azure Automation 계정 관리</span><span class="sxs-lookup"><span data-stu-id="4fcfe-103">Manage Azure Automation account</span></span>
<span data-ttu-id="4fcfe-104">Automation 계정 만료되기 전인 어떤 시점에서 인증서를 갱신해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-104">At some point before your Automation account expires, you will need to renew the certificate.</span></span> <span data-ttu-id="4fcfe-105">실행 계정이 손상되었다고 생각하시면 삭제하고 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-105">If you believe that the Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="4fcfe-106">이 섹션에서는 이러한 작업을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-106">This section discusses how to perform these operations.</span></span>

## <a name="self-signed-certificate-renewal"></a><span data-ttu-id="4fcfe-107">자체 서명된 인증서 갱신</span><span class="sxs-lookup"><span data-stu-id="4fcfe-107">Self-signed certificate renewal</span></span>
<span data-ttu-id="4fcfe-108">실행 계정에 만든 자체 서명된 인증서는 생성 날짜로부터 1년이 되는 날에 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-108">The self-signed certificate that you created for the Run As account expires one year from the date of creation.</span></span> <span data-ttu-id="4fcfe-109">만료되기 전에 언제든지 갱신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-109">You can renew it at any time before it expires.</span></span> <span data-ttu-id="4fcfe-110">인증서를 갱신하면 큐에 대기하거나 활발하게 실행 중이며 실행 계정으로 인증되는 모든 Runbook이 부정적인 영향을 받지 않도록 현재 유효한 인증서가 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-110">When you renew it, the current valid certificate is retained to ensure that any runbooks that are queued up or actively running, and that authenticate with the Run As account, are not negatively affected.</span></span> <span data-ttu-id="4fcfe-111">인증서는 만료 날짜까지 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-111">The certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="4fcfe-112">엔터프라이즈 인증 기관에서 발급한 인증서를 사용하도록 Automation 실행 계정을 구성하고 이 옵션을 사용하는 경우 엔터프라이즈 인증서는 자체 서명된 인증서로 교체됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-112">If you have configured your Automation Run As account to use a certificate issued by your enterprise certificate authority and you use this option, the enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="4fcfe-113">인증서를 갱신하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-113">To renew the certificate, do the following:</span></span>

1. <span data-ttu-id="4fcfe-114">Azure Portal에서 Automation 계정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-114">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="4fcfe-115">**Automation 계정** 블레이드의 **계정 속성** 창에서 **계정 설정** 섹션 아래에 있는 **실행 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-115">On the **Automation Account** blade, in the **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Automation 계정 속성 창](media/automation-manage-account/automation-account-properties-pane.png)
3. <span data-ttu-id="4fcfe-117">**실행 계정** 속성 블레이드에서 인증서를 갱신하려는 실행 계정 또는 클래식 실행 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-117">On the **Run As Accounts** properties blade, select either the Run As account or the Classic Run As account that you want to renew the certificate for.</span></span>

4. <span data-ttu-id="4fcfe-118">선택한 계정의 **속성** 블레이드에서 **인증서 갱신**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-118">On the **Properties** blade for the selected account, click **Renew certificate**.</span></span>

    ![실행 계정용 인증서 갱신](media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="4fcfe-120">인증서가 갱신되는 동안 메뉴의 **알림**에서 진행률을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-120">While the certificate is being renewed, you can track the progress under **Notifications** from the menu.</span></span>

## <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="4fcfe-121">실행 또는 클래식 실행 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="4fcfe-121">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="4fcfe-122">이 섹션에서는 실행 또는 클래식 실행 계정을 삭제하고 다시 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-122">This section describes how to delete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="4fcfe-123">이 작업을 실행하는 경우 Automation 계정이 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-123">When you perform this action, the Automation account is retained.</span></span> <span data-ttu-id="4fcfe-124">실행 또는 클래식 실행 계정을 삭제한 후에 Azure Portal에서 계정을 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-124">After you delete a Run As or Classic Run As account, you can re-create it in the Azure portal.</span></span>

1. <span data-ttu-id="4fcfe-125">Azure Portal에서 Automation 계정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-125">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="4fcfe-126">**Automation 계정** 블레이드의 계정 속성 창에서 **실행 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-126">On the **Automation account** blade, in the account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="4fcfe-127">**실행 계정** 속성 블레이드에서 삭제하려는 실행 계정 또는 클래식 실행 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-127">On the **Run As Accounts** properties blade, select either the Run As account or Classic Run As account that you want to delete.</span></span> <span data-ttu-id="4fcfe-128">그런 다음 선택한 계정의 **속성** 블레이드에서 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-128">Then, on the **Properties** blade for the selected account, click **Delete**.</span></span>

 ![실행 계정 삭제](media/automation-manage-account/automation-account-delete-runas.png)

4. <span data-ttu-id="4fcfe-130">계정이 삭제되는 동안 메뉴의 **알림** 에서 진행률을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-130">While the account is being deleted, you can track the progress under **Notifications** from the menu.</span></span>

5. <span data-ttu-id="4fcfe-131">계정이 삭제되면 **실행 계정** 속성 블레이드에서 **Azure 실행 계정** 만들기 옵션을 선택하여 계정을 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-131">After the account has been deleted, you can re-create it on the **Run As Accounts** properties blade by selecting the create option **Azure Run As Account**.</span></span>

 ![Automation 실행 계정 다시 만들기](media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a><span data-ttu-id="4fcfe-133">잘못된 구성</span><span class="sxs-lookup"><span data-stu-id="4fcfe-133">Misconfiguration</span></span>
<span data-ttu-id="4fcfe-134">실행 또는 클래식 실행 계정이 제대로 작동하는 데 필요한 일부 구성 항목이 초기 설정 중에 제대로 삭제되거나 생성되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-134">Some configuration items necessary for the Run As or Classic Run As account to function properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="4fcfe-135">항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-135">The items include:</span></span>

* <span data-ttu-id="4fcfe-136">인증서 자산</span><span class="sxs-lookup"><span data-stu-id="4fcfe-136">Certificate asset</span></span>
* <span data-ttu-id="4fcfe-137">연결 자산</span><span class="sxs-lookup"><span data-stu-id="4fcfe-137">Connection asset</span></span>
* <span data-ttu-id="4fcfe-138">실행 계정이 참여자 역할에서 제거됨</span><span class="sxs-lookup"><span data-stu-id="4fcfe-138">Run As account has been removed from the contributor role</span></span>
* <span data-ttu-id="4fcfe-139">Azure AD의 서비스 주체 또는 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="4fcfe-139">Service principal or application in Azure AD</span></span>

<span data-ttu-id="4fcfe-140">잘못된 구성의 이전 및 다른 인스턴스에서 Automation 계정은 변경 사항을 감지하고 계정의 **실행 계정** 속성 블레이드에서 *불완전*이라는 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-140">In the preceding and other instances of misconfiguration, the Automation account detects the changes and displays a status of *Incomplete* on the **Run As Accounts** properties blade for the account.</span></span>

![불완전 실행 계정 구성 상태](media/automation-manage-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="4fcfe-142">실행 계정을 선택하면 계정 **속성** 창은 다음과 같은 오류 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-142">When you select the Run As account, the account **Properties** pane displays the following error message:</span></span>

![불완전 실행 계정 구성 경고 메시지](media/automation-manage-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="4fcfe-144">등 4가지 유형의 클러스터가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-144">.</span></span>

<span data-ttu-id="4fcfe-145">계정을 삭제하고 다시 만들어서 이러한 실행 계정 문제를 신속하게 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-145">You can quickly resolve these Run As account issues by deleting and re-creating the account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fcfe-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4fcfe-146">Next steps</span></span>
* <span data-ttu-id="4fcfe-147">서비스 주체에 대한 자세한 내용은 [응용 프로그램 개체 및 서비스 주체 개체](../active-directory/active-directory-application-objects.md)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-147">For more information about Service Principals, refer to [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="4fcfe-148">Azure 자동화의 역할 기반 액세스 제어에 대한 자세한 내용은 [Azure 자동화에서 역할 기반 액세스 제어](automation-role-based-access-control.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-148">For more information about Role-based Access Control in Azure Automation, refer to [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="4fcfe-149">인증서 및 Azure 서비스에 대한 자세한 내용은 [Azure Cloud Services 인증서 개요](../cloud-services/cloud-services-certs-create.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4fcfe-149">For more information about certificates and Azure services, refer to [Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>