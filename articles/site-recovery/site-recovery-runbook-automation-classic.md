---
title: "클래식 포털에서 복구 계획에 Azure 자동화 Runbook 추가 | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery에서 Azure 자동화를 사용하여 복구 계획을 확장하여 Azure로 복구하는 동안 복잡한 작업을 완료할 수 있도록 하는 방법을 설명합니다."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: f24eaa62-9dea-4fce-92e1-a72513ca0289
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 0a248e7c3f39a35ac10dc6ac64e5cef7d152e033
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="add-azure-automation-runbooks-to-recovery-plans-in-the-classic-portal"></a><span data-ttu-id="0b56c-103">클래식 포털에서 복구 계획에 Azure 자동화 Runbook 추가</span><span class="sxs-lookup"><span data-stu-id="0b56c-103">Add Azure automation runbooks to recovery plans in the classic portal</span></span>
<span data-ttu-id="0b56c-104">이 자습서에서는 Azure Site Recovery가 복구 계획에 확장성을 제공하는 Azure 자동화와 통합하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-104">This tutorial describes how Azure Site Recovery integrates with Azure Automation to provide extensibility to recovery plans.</span></span> <span data-ttu-id="0b56c-105">복구 계획은 보조 클라우드에 복제 및 Azure 시나리오에 복제 둘 다에 Azure Site Recovery를 사용하여 보호되는 가상 컴퓨터의 복구를 오케스트레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-105">Recovery plans can orchestrate recovery of your virtual machines protected using Azure Site Recovery for both replication to secondary cloud and replication to Azure scenarios.</span></span> <span data-ttu-id="0b56c-106">복구를 **일관적으로 정확**하고, **반복 가능**하며, **자동화**되도록 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-106">They also help in making the recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="0b56c-107">Azure에 가상 컴퓨터의 장애를 복구하는 경우, Azure 자동화와의 통합은 복구 계획을 확대하고 runbook을 실행하는 기능을 제공하므로 강력한 자동화 작업이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-107">If you are failing over your virtual machines to Azure, integration with Azure Automation extends the recovery plans and gives you capability to execute runbooks, thus allowing powerful automation tasks.</span></span>

<span data-ttu-id="0b56c-108">Azure Automation에 대해 아직 들어보지 못한 경우 [여기](https://azure.microsoft.com/services/automation/)에 등록하여 [여기](https://azure.microsoft.com/documentation/scripts/)에서 샘플 스크립트를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-108">If you have not heard about Azure Automation yet, sign up [here](https://azure.microsoft.com/services/automation/) and download their sample scripts [here](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="0b56c-109">[여기](https://azure.microsoft.com/blog/?p=166264)에서 [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) 및 복구 계획을 사용하여 Azure에 복구를 오케스트레이션하는 방법에 대해 더 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-109">Read more about [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) and how to orchestrate recovery to Azure using recovery plans [here](https://azure.microsoft.com/blog/?p=166264).</span></span>

<span data-ttu-id="0b56c-110">이 짧은 자습서에서는 Azure Automation runbook을 복구 계획에 통합하는 방법에 대해 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-110">In this short tutorial, we will look at how you can integrate Azure Automation runbooks into recovery plans.</span></span> <span data-ttu-id="0b56c-111">앞서 수동 개입이 필요한 단순한 작업을 자동화하고 여러 단계의 복구를 클릭 한 번의 복구 동작으로 변환하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-111">We will automate simple tasks that earlier required manual intervention and see how to convert a multi step recovery into a single-click recovery action.</span></span> <span data-ttu-id="0b56c-112">문제가 발생하는 경우 간단한 스크립트 문제를 해결하는 방법에 대해서도 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-112">We will also look at how you can troubleshoot a simple script if it goes wrong.</span></span>

## <a name="protect-the-application-to-azure"></a><span data-ttu-id="0b56c-113">Azure로 응용프로그램 보호</span><span class="sxs-lookup"><span data-stu-id="0b56c-113">Protect the application to Azure</span></span>
<span data-ttu-id="0b56c-114">두 가상 컴퓨터로 구성되는 간단한 응용프로그램으로 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-114">Let us begin with a simple application consisting of two virtual machines.</span></span> <span data-ttu-id="0b56c-115">여기서는 Fabrikam의 HRweb 응용프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-115">Here, we have a HRweb application of Fabrikam.</span></span> <span data-ttu-id="0b56c-116">Fabrikam-HRweb-프런트엔드 및 Fabrikam-Hrweb-백엔드는 Azure Site Recovery를 사용하여 Azure로 보호되는 두 가상 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-116">Fabrikam-HRweb-frontend and Fabrikam-Hrweb-backend are the two virtual machines protected to Azure using Azure Site Recovery.</span></span> <span data-ttu-id="0b56c-117">Azure Site Recovery를 사용하여 가상 컴퓨터를 보호하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-117">To protect the virtual machines using Azure Site Recovery, follow the steps below.</span></span>

1. <span data-ttu-id="0b56c-118">가상 컴퓨터의 보호를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-118">Enable protection for your virtual machines.</span></span>
2. <span data-ttu-id="0b56c-119">가상 컴퓨터가 초기 복제를 완료했고 복제 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-119">Ensure that the virtual machines have completed initial replication and are replicating.</span></span>
3. <span data-ttu-id="0b56c-120">초기 복제를 완료할 때까지 기다리면 복제 상태가 보호됨이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-120">Wait till the initial replication completes and the Replication status says Protected.</span></span>

## ![](media/site-recovery-runbook-automation/01.png)
<span data-ttu-id="0b56c-121">이 자습서에서는 Azure로 응용프로그램 장애 조치를 하도록 Fabrikam HRweb 응용프로그램에 대한 복구 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-121">In this tutorial, we will create a recovery plan for the Fabrikam HRweb application to failover the application to Azure.</span></span> <span data-ttu-id="0b56c-122">그런 다음 포트 80에서 웹 페이지를 제공하여 장애를 복구한 Azure 가상 컴퓨터에 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-122">Then we will integrate it with a runbook that will create an endpoint on the failed over Azure virtual machine to serve web pages at port 80.</span></span>

<span data-ttu-id="0b56c-123">먼저, 응용프로그램에 대한 복구 계획을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-123">First, let's create a recovery plan for our application.</span></span>

## <a name="create-the-recovery-plan"></a><span data-ttu-id="0b56c-124">복구 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="0b56c-124">Create the recovery plan</span></span>
<span data-ttu-id="0b56c-125">Azure에 응용프로그램을 복구하려면 복구 계획을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-125">To recover the application to Azure, you need to create a recovery plan.</span></span>
<span data-ttu-id="0b56c-126">복구 계획을 사용하여 가상 컴퓨터 복구 순서를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-126">Using a recovery plan you can specify the order of recovery of the virtual machines.</span></span> <span data-ttu-id="0b56c-127">그룹 1에 배치된 가상 컴퓨터는 먼저 복구를 시작하며 그룹 2의 가상 컴퓨터가 이어서 복구됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-127">The virtual machine placed in group 1 will recover and start first, and then the virtual machine in group 2 will follow.</span></span>

<span data-ttu-id="0b56c-128">아래와 같이 복구 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-128">Create a Recovery Plan that looks like below.</span></span>

![](media/site-recovery-runbook-automation/12.png)

<span data-ttu-id="0b56c-129">복구 계획에 대한 자세한 내용은 [여기](https://msdn.microsoft.com/library/azure/dn788799.aspx "여기")되도록 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-129">To read more about recovery plans, read documentation [here](https://msdn.microsoft.com/library/azure/dn788799.aspx "here").</span></span>

<span data-ttu-id="0b56c-130">다음으로, Azure 자동화에서 필요한 아티팩트를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-130">Next, let's create the necessary artifacts in Azure Automation.</span></span>

## <a name="create-the-automation-account-and-its-assets"></a><span data-ttu-id="0b56c-131">자동화 계정 및 해당 자산 만들기</span><span class="sxs-lookup"><span data-stu-id="0b56c-131">Create the automation account and its assets</span></span>
<span data-ttu-id="0b56c-132">runbook을 만들려면 Azure 자동화 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-132">You need an Azure Automation account to create runbooks.</span></span> <span data-ttu-id="0b56c-133">계정이 아직 없는 경우 ![](media/site-recovery-runbook-automation/02.png)(으)로 표시된 Azure 자동화 탭으로 이동하여 새 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-133">If you do not already have an account, navigate to Azure Automation tab denoted by ![](media/site-recovery-runbook-automation/02.png)and create a new account.</span></span>

1. <span data-ttu-id="0b56c-134">식별하는 이름으로 계정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-134">Give the account a name to identify with.</span></span>
2. <span data-ttu-id="0b56c-135">해당 계정을 배치하려는 지리적 영역을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-135">Specify a geographical region where you want to place the account.</span></span>

<span data-ttu-id="0b56c-136">ASR 자격 증명 모음과 동일한 하위 지역에 계정을 배치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-136">It is recommended to place the account in the same region as the ASR vault.</span></span>

![](media/site-recovery-runbook-automation/03.png)

<span data-ttu-id="0b56c-137">다음으로, 계정에서 다음 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-137">Next, create the following assets in the Account.</span></span>

### <a name="add-a-subscription-name-as-asset"></a><span data-ttu-id="0b56c-138">자산으로 구독 이름 추가</span><span class="sxs-lookup"><span data-stu-id="0b56c-138">Add a subscription name as asset</span></span>
1. <span data-ttu-id="0b56c-139">Azure 자동화 자산에 새 설정 ![](media/site-recovery-runbook-automation/04.png)을(를) 추가하고 ![](media/site-recovery-runbook-automation/05.png) 선택</span><span class="sxs-lookup"><span data-stu-id="0b56c-139">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in the Azure Automation Assets and select to ![](media/site-recovery-runbook-automation/05.png)</span></span>
2. <span data-ttu-id="0b56c-140">변수 유형을 **문자열**</span><span class="sxs-lookup"><span data-stu-id="0b56c-140">Select the variable type as **String**</span></span>
3. <span data-ttu-id="0b56c-141">변수 이름으로 **AzureSubscriptionName**</span><span class="sxs-lookup"><span data-stu-id="0b56c-141">Specify variable name as **AzureSubscriptionName**</span></span>

   ![](media/site-recovery-runbook-automation/06.png)
4. <span data-ttu-id="0b56c-142">실제 Azure 구독 이름을 변수 값으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-142">Specify your actual Azure Subscription name as the variable value.</span></span>

   ![](media/site-recovery-runbook-automation/07_1.png)

<span data-ttu-id="0b56c-143">Azure 포털의 계정 설정 페이지에서 구독 이름을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-143">You can identify the name of your subscription from the settings page of your account on the Azure portal.</span></span>

### <a name="add-an-azure-login-credential-as-asset"></a><span data-ttu-id="0b56c-144">Azure 로그인 자격 증명을 자산으로 추가</span><span class="sxs-lookup"><span data-stu-id="0b56c-144">Add an Azure login credential as asset</span></span>
<span data-ttu-id="0b56c-145">Azure 자동화는 Azure PowerShell을 사용하여 구독에 연결하고 해당 아티팩트에서 작업합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-145">Azure Automation uses Azure PowerShell to connect to the subscription and operates on the artifacts there.</span></span> <span data-ttu-id="0b56c-146">이를 위해 Microsoft 계정 또는 회사나 학교 계정을 사용하여 인증을 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-146">For this, you need to authenticate using your Microsoft account or a work or school account.</span></span>
<span data-ttu-id="0b56c-147">해당 runbook을 통해 안전하게 사용되는 자산에 계정 자격 증명을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-147">You can store the account credentials in an asset to be used securely by the runbook.</span></span>

1. <span data-ttu-id="0b56c-148">Azure 자동화 자산에 새 설정 ![](media/site-recovery-runbook-automation/04.png)을(를) 추가하고 ![](media/site-recovery-runbook-automation/09.png) 선택</span><span class="sxs-lookup"><span data-stu-id="0b56c-148">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in the Azure Automation Assets and select ![](media/site-recovery-runbook-automation/09.png)</span></span>
2. <span data-ttu-id="0b56c-149">자격 증명 형식을 **Windows PowerShell 자격 증명**</span><span class="sxs-lookup"><span data-stu-id="0b56c-149">Select the Credential type as **Windows PowerShell Credential**</span></span>
3. <span data-ttu-id="0b56c-150">이름을 **AzureCredential**</span><span class="sxs-lookup"><span data-stu-id="0b56c-150">Specify the name as **AzureCredential**</span></span>

   ![](media/site-recovery-runbook-automation/10.png)
4. <span data-ttu-id="0b56c-151">로그인할 사용자 이름 및 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-151">Specify the username and password to sign-in with.</span></span>

<span data-ttu-id="0b56c-152">이제 이러한 두 설정을 자산에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-152">Now both these settings are available in your assets.</span></span>

![](media/site-recovery-runbook-automation/11.png)

<span data-ttu-id="0b56c-153">PowerShell을 통해 구독에 연결하는 방법에 대한 자세한 내용은 [여기](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b56c-153">More information about how to connect to your subscription via PowerShell is given [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="0b56c-154">다음으로, 장애 조치 후 프런트엔드 가상 컴퓨터에 끝점을 추가할 수 있는 Azure 자동화에서 runbook을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-154">Next, you will create a runbook in Azure Automation that can add an endpoint for the front-end virtual machine after failover.</span></span>

## <a name="azure-automation-context"></a><span data-ttu-id="0b56c-155">Azure 자동화 컨텍스트</span><span class="sxs-lookup"><span data-stu-id="0b56c-155">Azure automation context</span></span>
<span data-ttu-id="0b56c-156">ASR은 결정적 스크립트를 작성할 수 있도록 runbook에 컨텍스트 변수를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-156">ASR passes a context variable to the runbook to help you write deterministic scripts.</span></span> <span data-ttu-id="0b56c-157">클라우드 서비스 및 가상 컴퓨터의 이름을 보호할 수 있음을 입증하지만, Azure에서 지원되지 않는 문자로 인해 변경될 수 있는 가상 컴퓨터의 이름이 있는 특정 시나리오 때문에 항상 그렇지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-157">One could argue that the names of the Cloud Service and the Virtual Machine are predictable, but happens that it is not always the case owing to certain scenarios such as the one where the name of the virtual machine name might have changed due to unsupported characters in Azure.</span></span> <span data-ttu-id="0b56c-158">따라서 이 정보는 *컨텍스트*의 일부로 ASR 복구 계획에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-158">Hence this information is passed to the ASR recovery plan as part of the *context*.</span></span>

<span data-ttu-id="0b56c-159">다음은 컨텍스트 변수를 표시하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-159">Below is an example of how the context variable looks.</span></span>

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


<span data-ttu-id="0b56c-160">아래 표에는 컨텍스트의 각 변수에 대한 이름과 설명이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-160">The table below contains name and description for each variable in the context.</span></span>

| <span data-ttu-id="0b56c-161">**변수 이름**</span><span class="sxs-lookup"><span data-stu-id="0b56c-161">**Variable name**</span></span> | <span data-ttu-id="0b56c-162">**설명**</span><span class="sxs-lookup"><span data-stu-id="0b56c-162">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="0b56c-163">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="0b56c-163">RecoveryPlanName</span></span> |<span data-ttu-id="0b56c-164">실행되는 계획의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-164">Name of plan being run.</span></span> <span data-ttu-id="0b56c-165">동일한 스크립트를 사용하는 이름에 따라 필요한 조치를 취할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-165">Helps you take action based on name using the same script</span></span> |
| <span data-ttu-id="0b56c-166">FailoverType</span><span class="sxs-lookup"><span data-stu-id="0b56c-166">FailoverType</span></span> |<span data-ttu-id="0b56c-167">장애 조치(failover)가 테스트, 계획됨 또는 계획되지 않음인지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-167">Specifies whether the failover is test, planned, or unplanned.</span></span> |
| <span data-ttu-id="0b56c-168">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="0b56c-168">FailoverDirection</span></span> |<span data-ttu-id="0b56c-169">복구가 주 사이트 쪽으로 이루어지는지 보조 사이트 쪽으로 이루어지는지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-169">Specify whether recovery is to primary or secondary</span></span> |
| <span data-ttu-id="0b56c-170">GroupID</span><span class="sxs-lookup"><span data-stu-id="0b56c-170">GroupID</span></span> |<span data-ttu-id="0b56c-171">계획이 실행 중일 때 복구 계획 내의 그룹 번호를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-171">Identify the group number within the recovery plan when the plan is running</span></span> |
| <span data-ttu-id="0b56c-172">VmMap</span><span class="sxs-lookup"><span data-stu-id="0b56c-172">VmMap</span></span> |<span data-ttu-id="0b56c-173">그룹에 있는 모든 가상 컴퓨터의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-173">Array of all the virtual machines in the group</span></span> |
| <span data-ttu-id="0b56c-174">VMMap key</span><span class="sxs-lookup"><span data-stu-id="0b56c-174">VMMap key</span></span> |<span data-ttu-id="0b56c-175">각 VM에 대한 고유 키(GUID)입니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-175">Unique key (GUID) for each VM.</span></span> <span data-ttu-id="0b56c-176">해당되는 경우 가상 컴퓨터의 VMM ID와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-176">It's the same as the VMM ID of the virtual machine where applicable.</span></span> |
| <span data-ttu-id="0b56c-177">RoleName</span><span class="sxs-lookup"><span data-stu-id="0b56c-177">RoleName</span></span> |<span data-ttu-id="0b56c-178">복구 중인 Azure VM의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-178">Name of the Azure VM that's being recovered</span></span> |
| <span data-ttu-id="0b56c-179">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="0b56c-179">CloudServiceName</span></span> |<span data-ttu-id="0b56c-180">가상 컴퓨터가 만들어지는 Azure 클라우드 서비스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-180">Azure Cloud Service name under which the virtual machine is created.</span></span> |

<span data-ttu-id="0b56c-181">컨텍스트에서 VmMap 키를 식별하려면 ASR에서 VM 속성 페이지로 이동하여 VM GUID 속성을 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-181">To identify the VmMap Key in the context you could also go to the VM properties page in ASR and look at the VM GUID property.</span></span>

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a><span data-ttu-id="0b56c-182">자동화 Runbook 작성</span><span class="sxs-lookup"><span data-stu-id="0b56c-182">Author an Automation runbook</span></span>
<span data-ttu-id="0b56c-183">이제 프런트엔드 가상 컴퓨터에서 포트 80을 열기 위해 runbook을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-183">Now create the runbook to open port 80 on the front-end virtual machine.</span></span>

1. <span data-ttu-id="0b56c-184">**OpenPort80**</span><span class="sxs-lookup"><span data-stu-id="0b56c-184">Create a new runbook in the Azure Automation account with the name **OpenPort80**</span></span>

   ![](media/site-recovery-runbook-automation/14.png)
2. <span data-ttu-id="0b56c-185">runbook의 작성자 보기로 이동하여 초안 모드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-185">Navigate to the Author view of the runbook and enter the draft mode.</span></span>
3. <span data-ttu-id="0b56c-186">먼저, 복구 계획 컨텍스트로 사용할 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-186">First specify the variable to use as the recovery plan context</span></span>

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. <span data-ttu-id="0b56c-187">그런 다음, 자격 증명 및 구독 이름을 사용하여 구독에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-187">Next connect to the subscription using the credential and subscription name</span></span>

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect to Azure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   <span data-ttu-id="0b56c-188">여기에서 Azure 자산, **AzureCredential** 및 **AzureSubscriptionName**을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-188">Note that you use the Azure assets – **AzureCredential** and **AzureSubscriptionName** here.</span></span>
5. <span data-ttu-id="0b56c-189">이제 끝점을 노출하려는 가상 컴퓨터의 GUID 및 끝점 세부 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-189">Now specify the endpoint details and the GUID of the virtual machine for which you want to expose the endpoint.</span></span> <span data-ttu-id="0b56c-190">이 경우 프런트엔드 가상 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-190">In this case the front-end virtual machine.</span></span>

   ```
       # Specify the parameters to be used by the script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   <span data-ttu-id="0b56c-191">Azure 끝점 프로토콜, VM의 로컬 포트 및 매핑된 해당 공용 포트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-191">This specifies the Azure endpoint protocol, local port on the VM and its mapped public port.</span></span> <span data-ttu-id="0b56c-192">이러한 변수는 VM에 끝점을 추가하는 Azure 명령에 필요한 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-192">These variables are parameters     required by the Azure commands that add endpoints to VMs.</span></span> <span data-ttu-id="0b56c-193">VMGUID는 작동에 필요한 가상 컴퓨터의 GUID를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-193">The VMGUID holds the GUID of the virtual machine you need to operate on.</span></span>
6. <span data-ttu-id="0b56c-194">스크립트는 이제 지정한 VM GUID에 대한 컨텍스트를 추출하여 이를 통해 참조되는 가상 컴퓨터에 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-194">The script will now extract the context for the given VM GUID and create an endpoint on the virtual machine referenced by it.</span></span>

   ```
       #Read the VM GUID from the context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke the necessary pipeline commands to add a Azure Endpoint to a specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. <span data-ttu-id="0b56c-195">이 작업이 완료되면 게시 ![](media/site-recovery-runbook-automation/20.png) 를 눌러 스크립트를 실행에 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-195">Once this is complete, hit Publish ![](media/site-recovery-runbook-automation/20.png) to allow your script to be available for execution.</span></span>

<span data-ttu-id="0b56c-196">전체 스크립트는 참조를 위해 아래에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-196">The complete script is given below for your reference</span></span>

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect to Azure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify the parameters to be used by the script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read the VM GUID from the context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke the necessary pipeline commands to add an Azure Endpoint to a specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-the-script-to-the-recovery-plan"></a><span data-ttu-id="0b56c-197">복구 계획에 스크립트 추가</span><span class="sxs-lookup"><span data-stu-id="0b56c-197">Add the script to the recovery plan</span></span>
<span data-ttu-id="0b56c-198">스크립트가 준비되면 앞서 만든 복구 계획에 이를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-198">Once the script is ready, you can add it to the recovery plan that you created earlier.</span></span>

1. <span data-ttu-id="0b56c-199">만든 복구 계획에서 그룹 2 다음에 스크립트를 추가하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-199">In the recovery plan you created, choose to add a script after the group 2.</span></span> ![](media/site-recovery-runbook-automation/15.png)
2. <span data-ttu-id="0b56c-200">스크립트 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-200">Specify a script name.</span></span> <span data-ttu-id="0b56c-201">복구 계획 내에 표시하기 위한 이 스크립트의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-201">This is just a friendly name for this script for showing within the Recovery plan.</span></span>
3. <span data-ttu-id="0b56c-202">Azure 스크립트에 대한 장애 조치에서 Azure 자동화 계정 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-202">In the failover to Azure script – Select the Azure Automation Account name.</span></span>
4. <span data-ttu-id="0b56c-203">Azure Runbook에서 작성한 runbook을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-203">In the Azure Runbooks, select the runbook you authored.</span></span>

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a><span data-ttu-id="0b56c-204">기본 측 스크립트</span><span class="sxs-lookup"><span data-stu-id="0b56c-204">Primary side scripts</span></span>
<span data-ttu-id="0b56c-205">Azure에 장애 조치(Failover)를 실행할 때 기본 측 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-205">When you are executing a failover to Azure, you can also choose to execute primary side scripts.</span></span> <span data-ttu-id="0b56c-206">이러한 스크립트는 장애 조치(Failover) 중 VMM 서버에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-206">These scripts will run on the VMM server during failover.</span></span>
<span data-ttu-id="0b56c-207">기본 측 스크립트는 종료 전 및 종료 후 단계에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-207">Primary side scripts are only available only for pre-shutdown and post shutdown stages.</span></span> <span data-ttu-id="0b56c-208">그 이유는 재해가 발생할 경우 일반적으로 기본 사이트를 사용할 수 없다고 예상하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-208">This is because we expect the primary site to be typically unavailable when a disaster strikes.</span></span>
<span data-ttu-id="0b56c-209">계획되지 않은 장애 조치(Failover) 중에는 기본 사이트 작업을 선택할 경우에만 기본 측 스크립트 실행을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-209">During an unplanned failover, only if you opt in for primary site operations, it will attempt to run the primary side scripts.</span></span> <span data-ttu-id="0b56c-210">연결할 수 없거나 시간이 초과되는 경우 장애 조치(Failover)에서 계속 가상 컴퓨터를 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-210">If they are not reachable or timeout, the failover will continue to recover the virtual machines.</span></span>
<span data-ttu-id="0b56c-211">Azure로 장애 조치(Failover)를 실행하는 동안 Azure에 대해 보호된 VMM이 없으면 VMware/물리/Hyper-v 사이트에서 기본 측 스크립트를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-211">Primary side scripts are un-available for VMware/Physical/Hyper-v Sites without VMM protected to Azure - while you failover to Azure.</span></span>
<span data-ttu-id="0b56c-212">하지만 Azure에서 온-프레미스로 장애 조치(Failover)를 실행할 경우에는 VMware를 제외한 모든 대상에 기본 측 스크립트(Runbook)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-212">However, when you failback from Azure to on-premises, primary side scripts (Runbooks) can be used for all targets except VMware.</span></span>

## <a name="test-the-recovery-plan"></a><span data-ttu-id="0b56c-213">복구 계획 테스트</span><span class="sxs-lookup"><span data-stu-id="0b56c-213">Test the recovery plan</span></span>
<span data-ttu-id="0b56c-214">계획에 runbook을 추가하면 테스트 장애 조치를 초기화하고 동작에서 이를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-214">Once you have added the runbook to the plan you can initiate a test failover and see it in action.</span></span> <span data-ttu-id="0b56c-215">오류가 없도록 복구 계획 및 응용프로그램을 테스트하도록 테스트 장애 조치를 실행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-215">It is always recommended to run a test failover to test your application and the recovery plan to ensure that there are no errors.</span></span>

1. <span data-ttu-id="0b56c-216">복구 계획을 선택하고 테스트 장애 조치를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-216">Select the recovery plan and initiate a test failover.</span></span>
2. <span data-ttu-id="0b56c-217">계획을 실행하는 동안 해당 상태를 통해 runbook의 실행 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-217">During the plan execution, you can see whether the runbook has executed or not via its status.</span></span>

   ![](media/site-recovery-runbook-automation/17.png)
3. <span data-ttu-id="0b56c-218">runbook에 대해 Azure 자동화 작업 페이지에서 자세한 runbook 실행 상태를 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-218">You can also see the detailed runbook execution status on the Azure Automation jobs page for the runbook.</span></span>

   ![](media/site-recovery-runbook-automation/18.png)
4. <span data-ttu-id="0b56c-219">runbook 실행 결과 외에도 장애 조치를 완료한 후에 Azure 가상 컴퓨터 페이지를 방문하여 끝점을 살펴봄으로써 실행 성공 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-219">After the failover completes, apart from the runbook execution result, you can see whether the execution is successful or not by visiting the Azure virtual machine page and looking at the endpoints.</span></span>

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a><span data-ttu-id="0b56c-220">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="0b56c-220">Sample scripts</span></span>
<span data-ttu-id="0b56c-221">이 자습서에서 Azure 가상 컴퓨터에 끝점을 추가하는 일반적인 작업을 자동화하는 과정을 통해 Azure 자동화를 사용하여 그 밖의 강력한 자동화 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-221">While we walked through automating one commonly used task of adding an endpoint to an Azure virtual machine in this tutorial, you could do a number of other powerful automation tasks using Azure automation.</span></span> <span data-ttu-id="0b56c-222">Microsoft 및 Azure 자동화 커뮤니티에서는 사용자 고유의 솔루션 만들기를 시작하는 데 도움이 되는 샘플 Runbook 및 대규모 자동화 작업을 위한 구성 요소로 사용할 수 있는 유틸리티 Runbook을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-222">Microsoft and the Azure Automation community provide sample runbooks which can help you get started creating your own solutions, and utility runbooks, which you can use as building blocks for larger automation tasks.</span></span> <span data-ttu-id="0b56c-223">갤러리에서 사용을 시작하고 Azure Site Recovery를 사용하여 응용프로그램에 대한 강력한 원클릭 복구 계획을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0b56c-223">Start using them from the gallery and build  powerful one-click recovery plans for your applications using Azure Site Recovery.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0b56c-224">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="0b56c-224">Additional Resources</span></span>
[<span data-ttu-id="0b56c-225">Azure 자동화 개요</span><span class="sxs-lookup"><span data-stu-id="0b56c-225">Azure Automation Overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Azure 자동화 개요")

[<span data-ttu-id="0b56c-226">Azure 자동화 스크립트 샘플</span><span class="sxs-lookup"><span data-stu-id="0b56c-226">Sample Azure Automation Scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Azure 자동화 스크립트 샘플")
