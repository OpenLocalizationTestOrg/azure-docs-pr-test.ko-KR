---
title: "hello 클래식 포털에서 Azure 자동화 runbook toorecovery 계획 aaaAdd | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery 지금 사용 하 여 방법을 tooAzure 복구 하는 동안 Azure 자동화 toocomplete 복잡 한 작업을 사용 하 여 tooextend 복구 계획 설명"
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
ms.openlocfilehash: 3bb7420911afbce289b656f28823b1923e8af0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans-in-hello-classic-portal"></a><span data-ttu-id="70b7a-103">Hello 클래식 포털에서 Azure 자동화 runbook toorecovery 계획 추가</span><span class="sxs-lookup"><span data-stu-id="70b7a-103">Add Azure automation runbooks toorecovery plans in hello classic portal</span></span>
<span data-ttu-id="70b7a-104">이 자습서에서는 Azure 자동화 tooprovide 확장성 toorecovery 계획과 Azure Site Recovery 통합 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-104">This tutorial describes how Azure Site Recovery integrates with Azure Automation tooprovide extensibility toorecovery plans.</span></span> <span data-ttu-id="70b7a-105">복구 계획에는 가상 컴퓨터 복제 toosecondary 클라우드와 복제 tooAzure 시나리오 둘 다에 대 한 Azure Site Recovery를 사용 하 여 보호의 복구를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-105">Recovery plans can orchestrate recovery of your virtual machines protected using Azure Site Recovery for both replication toosecondary cloud and replication tooAzure scenarios.</span></span> <span data-ttu-id="70b7a-106">또한 hello 복구 될 때 지원할 **일관 되 게 정확한**, **반복 가능한**, 및 **자동화 된**합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-106">They also help in making hello recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="70b7a-107">가상 컴퓨터 tooAzure를 통해 실패 하는 경우 Azure 자동화와의 통합 복구 계획을 확장 하 고 강력한 자동화 작업 수 있도록 기능 tooexecute runbook을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-107">If you are failing over your virtual machines tooAzure, integration with Azure Automation extends the recovery plans and gives you capability tooexecute runbooks, thus allowing powerful automation tasks.</span></span>

<span data-ttu-id="70b7a-108">Azure Automation에 대해 아직 들어보지 못한 경우 [여기](https://azure.microsoft.com/services/automation/)에 등록하여 [여기](https://azure.microsoft.com/documentation/scripts/)에서 샘플 스크립트를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-108">If you have not heard about Azure Automation yet, sign up [here](https://azure.microsoft.com/services/automation/) and download their sample scripts [here](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="70b7a-109">에 대해 자세히 알아보세요 [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) tooorchestrate 복구 tooAzure 복구를 사용 하 여 계획 하는 방법 및 [여기](https://azure.microsoft.com/blog/?p=166264)합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-109">Read more about [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) and how tooorchestrate recovery tooAzure using recovery plans [here](https://azure.microsoft.com/blog/?p=166264).</span></span>

<span data-ttu-id="70b7a-110">이 짧은 자습서에서는 Azure Automation runbook을 복구 계획에 통합하는 방법에 대해 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-110">In this short tutorial, we will look at how you can integrate Azure Automation runbooks into recovery plans.</span></span> <span data-ttu-id="70b7a-111">이전 직접 이동 해야 하는 간단한 작업을 자동화 하 고 tooconvert 다중 복구 단일 클릭 복구 작업을 실행 하는 방법을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-111">We will automate simple tasks that earlier required manual intervention and see how tooconvert a multi step recovery into a single-click recovery action.</span></span> <span data-ttu-id="70b7a-112">문제가 발생하는 경우 간단한 스크립트 문제를 해결하는 방법에 대해서도 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-112">We will also look at how you can troubleshoot a simple script if it goes wrong.</span></span>

## <a name="protect-hello-application-tooazure"></a><span data-ttu-id="70b7a-113">Hello 응용 프로그램 tooAzure 보호</span><span class="sxs-lookup"><span data-stu-id="70b7a-113">Protect hello application tooAzure</span></span>
<span data-ttu-id="70b7a-114">두 가상 컴퓨터로 구성되는 간단한 응용프로그램으로 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-114">Let us begin with a simple application consisting of two virtual machines.</span></span> <span data-ttu-id="70b7a-115">여기서는 Fabrikam의 HRweb 응용프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-115">Here, we have a HRweb application of Fabrikam.</span></span> <span data-ttu-id="70b7a-116">Fabrikam-HRweb-프런트 엔드 및 백 엔드 Hrweb-Fabrikam-hello 두 개의 가상 컴퓨터가 Azure Site Recovery를 사용 하 여 tooAzure 보호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-116">Fabrikam-HRweb-frontend and Fabrikam-Hrweb-backend are hello two virtual machines protected tooAzure using Azure Site Recovery.</span></span> <span data-ttu-id="70b7a-117">Azure Site Recovery를 사용 하 여 tooprotect hello 가상 컴퓨터는 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-117">tooprotect hello virtual machines using Azure Site Recovery, follow hello steps below.</span></span>

1. <span data-ttu-id="70b7a-118">가상 컴퓨터의 보호를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-118">Enable protection for your virtual machines.</span></span>
2. <span data-ttu-id="70b7a-119">Hello 가상 컴퓨터 초기 복제를 완료 하 고 복제 중인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-119">Ensure that hello virtual machines have completed initial replication and are replicating.</span></span>
3. <span data-ttu-id="70b7a-120">Hello 초기 복제가 완료 되 고 복제 상태 hello은 보호 된 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-120">Wait till hello initial replication completes and hello Replication status says Protected.</span></span>

## ![](media/site-recovery-runbook-automation/01.png)
<span data-ttu-id="70b7a-121">이 자습서에서는 Fabrikam HRweb 응용 프로그램 toofailover hello 응용 프로그램 tooAzure hello에 대 한 복구 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-121">In this tutorial, we will create a recovery plan for hello Fabrikam HRweb application toofailover hello application tooAzure.</span></span> <span data-ttu-id="70b7a-122">다음 우리는와 통합 하 runbook이 Azure 가상 컴퓨터에서 포트 80 웹 페이지를 tooserve 조치할 hello에 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-122">Then we will integrate it with a runbook that will create an endpoint on hello failed over Azure virtual machine tooserve web pages at port 80.</span></span>

<span data-ttu-id="70b7a-123">먼저, 응용프로그램에 대한 복구 계획을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-123">First, let's create a recovery plan for our application.</span></span>

## <a name="create-hello-recovery-plan"></a><span data-ttu-id="70b7a-124">Hello 복구 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="70b7a-124">Create hello recovery plan</span></span>
<span data-ttu-id="70b7a-125">toorecover hello 응용 프로그램 tooAzure toocreate 복구 계획 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-125">toorecover hello application tooAzure, you need toocreate a recovery plan.</span></span>
<span data-ttu-id="70b7a-126">가상 컴퓨터의 복구의 hello 순서를 지정할 수는 복구 계획을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-126">Using a recovery plan you can specify hello order of recovery of the virtual machines.</span></span> <span data-ttu-id="70b7a-127">그룹 1에에서 배치 하는 hello 가상 컴퓨터에서 복구 하 고, 첫 번째 실행 합니다 및 다음 그룹 2의에서 가상 컴퓨터 hello 다룰 것입니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-127">hello virtual machine placed in group 1 will recover and start first, and then hello virtual machine in group 2 will follow.</span></span>

<span data-ttu-id="70b7a-128">아래와 같이 복구 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-128">Create a Recovery Plan that looks like below.</span></span>

![](media/site-recovery-runbook-automation/12.png)

<span data-ttu-id="70b7a-129">설명서를 참조 하는 복구 계획에 대 한 자세한 tooread [여기](https://msdn.microsoft.com/library/azure/dn788799.aspx "여기")합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-129">tooread more about recovery plans, read documentation [here](https://msdn.microsoft.com/library/azure/dn788799.aspx "here").</span></span>

<span data-ttu-id="70b7a-130">다음으로, 보겠습니다 Azure 자동화 hello 필요한 아티팩트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-130">Next, let's create hello necessary artifacts in Azure Automation.</span></span>

## <a name="create-hello-automation-account-and-its-assets"></a><span data-ttu-id="70b7a-131">Hello 자동화 계정 및 관련 자산 만들기</span><span class="sxs-lookup"><span data-stu-id="70b7a-131">Create hello automation account and its assets</span></span>
<span data-ttu-id="70b7a-132">Azure 자동화 계정 toocreate runbook이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-132">You need an Azure Automation account toocreate runbooks.</span></span> <span data-ttu-id="70b7a-133">계정이 아직 없는 경우 tooAzure 자동화 탭으로 표시 된 이동 ![](media/site-recovery-runbook-automation/02.png)새 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-133">If you do not already have an account, navigate tooAzure Automation tab denoted by ![](media/site-recovery-runbook-automation/02.png)and create a new account.</span></span>

1. <span data-ttu-id="70b7a-134">와 이름이 tooidentify hello 계정에 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-134">Give hello account a name tooidentify with.</span></span>
2. <span data-ttu-id="70b7a-135">저장할 tooplace hello 계정에서 지리적 위치 영역을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-135">Specify a geographical region where you want tooplace hello account.</span></span>

<span data-ttu-id="70b7a-136">Hello에 tooplace hello 계정 것이 좋습니다 hello ASR 자격 증명 모음과 동일한 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-136">It is recommended tooplace hello account in hello same region as hello ASR vault.</span></span>

![](media/site-recovery-runbook-automation/03.png)

<span data-ttu-id="70b7a-137">다음으로 hello 다음 hello 계정에에서 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-137">Next, create hello following assets in hello Account.</span></span>

### <a name="add-a-subscription-name-as-asset"></a><span data-ttu-id="70b7a-138">자산으로 구독 이름 추가</span><span class="sxs-lookup"><span data-stu-id="70b7a-138">Add a subscription name as asset</span></span>
1. <span data-ttu-id="70b7a-139">새 설정을 추가 ![](media/site-recovery-runbook-automation/04.png) 너무 선택한에 hello Azure 자동화 자산![](media/site-recovery-runbook-automation/05.png)</span><span class="sxs-lookup"><span data-stu-id="70b7a-139">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in hello Azure Automation Assets and select too![](media/site-recovery-runbook-automation/05.png)</span></span>
2. <span data-ttu-id="70b7a-140">Hello 변수 유형으로 **문자열**</span><span class="sxs-lookup"><span data-stu-id="70b7a-140">Select hello variable type as **String**</span></span>
3. <span data-ttu-id="70b7a-141">변수 이름으로 **AzureSubscriptionName**</span><span class="sxs-lookup"><span data-stu-id="70b7a-141">Specify variable name as **AzureSubscriptionName**</span></span>

   ![](media/site-recovery-runbook-automation/06.png)
4. <span data-ttu-id="70b7a-142">Hello 변수 값으로 실제 Azure 구독 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-142">Specify your actual Azure Subscription name as hello variable value.</span></span>

   ![](media/site-recovery-runbook-automation/07_1.png)

<span data-ttu-id="70b7a-143">Hello hello hello Azure 포털에서 사용자의 계정 설정 페이지에서에서 구독의 이름을 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-143">You can identify hello name of your subscription from hello settings page of your account on hello Azure portal.</span></span>

### <a name="add-an-azure-login-credential-as-asset"></a><span data-ttu-id="70b7a-144">Azure 로그인 자격 증명을 자산으로 추가</span><span class="sxs-lookup"><span data-stu-id="70b7a-144">Add an Azure login credential as asset</span></span>
<span data-ttu-id="70b7a-145">Azure 자동화 tooconnect toothe 구독 Azure PowerShell을 사용 하 고 있는 hello 아티팩트에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-145">Azure Automation uses Azure PowerShell tooconnect toothe subscription and operates on hello artifacts there.</span></span> <span data-ttu-id="70b7a-146">이를 위해 Microsoft 계정 또는 회사나 학교 계정을 사용하여 인증을 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-146">For this, you need to authenticate using your Microsoft account or a work or school account.</span></span>
<span data-ttu-id="70b7a-147">Hello runbook에서 안전 하 게 사용 하는 자산 toobe에 hello 계정 자격 증명을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-147">You can store hello account credentials in an asset toobe used securely by hello runbook.</span></span>

1. <span data-ttu-id="70b7a-148">새 설정을 추가 ![](media/site-recovery-runbook-automation/04.png) 에서 Azure 자동화 자산 hello 및 선택![](media/site-recovery-runbook-automation/09.png)</span><span class="sxs-lookup"><span data-stu-id="70b7a-148">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in hello Azure Automation Assets and select ![](media/site-recovery-runbook-automation/09.png)</span></span>
2. <span data-ttu-id="70b7a-149">자격 증명 유형으로 hello **Windows PowerShell 자격 증명**</span><span class="sxs-lookup"><span data-stu-id="70b7a-149">Select hello Credential type as **Windows PowerShell Credential**</span></span>
3. <span data-ttu-id="70b7a-150">Hello 이름으로 지정 **AzureCredential**</span><span class="sxs-lookup"><span data-stu-id="70b7a-150">Specify hello name as **AzureCredential**</span></span>

   ![](media/site-recovery-runbook-automation/10.png)
4. <span data-ttu-id="70b7a-151">Hello 사용자 이름 및 toosign에 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-151">Specify hello username and password toosign-in with.</span></span>

<span data-ttu-id="70b7a-152">이제 이러한 두 설정을 자산에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-152">Now both these settings are available in your assets.</span></span>

![](media/site-recovery-runbook-automation/11.png)

<span data-ttu-id="70b7a-153">PowerShell 통해 tooconnect tooyour 구독 지정 방법에 대 한 자세한 내용은 [여기](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-153">More information about how tooconnect tooyour subscription via PowerShell is given [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="70b7a-154">다음으로 장애 조치 후 hello 프런트 엔드 가상 컴퓨터에 대 한 끝점을 추가할 수 있는 Azure 자동화에서 runbook을 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-154">Next, you will create a runbook in Azure Automation that can add an endpoint for hello front-end virtual machine after failover.</span></span>

## <a name="azure-automation-context"></a><span data-ttu-id="70b7a-155">Azure 자동화 컨텍스트</span><span class="sxs-lookup"><span data-stu-id="70b7a-155">Azure automation context</span></span>
<span data-ttu-id="70b7a-156">ASR 전달 컨텍스트 변수 toohello runbook toohelp 결정적 스크립트를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-156">ASR passes a context variable toohello runbook toohelp you write deterministic scripts.</span></span> <span data-ttu-id="70b7a-157">Hello 클라우드 서비스 및 가상 컴퓨터 hello hello 이름을 예측할 수 있고 아닌지 항상 여기서 hello 가상 컴퓨터 이름의 hello 이름을 변경 했을 수 기한 하나 hello 같은 toocertain 시나리오 소유 하 고 있는 hello 경우 발생 하는 주장 수 하나 Azure에 toounsupported 문자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-157">One could argue that hello names of hello Cloud Service and hello Virtual Machine are predictable, but happens that it is not always hello case owing toocertain scenarios such as hello one where hello name of hello virtual machine name might have changed due toounsupported characters in Azure.</span></span> <span data-ttu-id="70b7a-158">따라서이 정보는 toohello ASR 복구 계획의 일부로 전달 되 hello *컨텍스트*합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-158">Hence this information is passed toohello ASR recovery plan as part of hello *context*.</span></span>

<span data-ttu-id="70b7a-159">다음은 hello 컨텍스트 변수의 표시 하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-159">Below is an example of how hello context variable looks.</span></span>

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


<span data-ttu-id="70b7a-160">hello 아래 표에서 이름 및 hello 컨텍스트에서 각 변수에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-160">hello table below contains name and description for each variable in hello context.</span></span>

| <span data-ttu-id="70b7a-161">**변수 이름**</span><span class="sxs-lookup"><span data-stu-id="70b7a-161">**Variable name**</span></span> | <span data-ttu-id="70b7a-162">**설명**</span><span class="sxs-lookup"><span data-stu-id="70b7a-162">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="70b7a-163">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="70b7a-163">RecoveryPlanName</span></span> |<span data-ttu-id="70b7a-164">실행되는 계획의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-164">Name of plan being run.</span></span> <span data-ttu-id="70b7a-165">사용 하 여 이름에 따라 작업을 수행 하는 데 도움이 됩니다. 동일한 hello 스크립트</span><span class="sxs-lookup"><span data-stu-id="70b7a-165">Helps you take action based on name using hello same script</span></span> |
| <span data-ttu-id="70b7a-166">FailoverType</span><span class="sxs-lookup"><span data-stu-id="70b7a-166">FailoverType</span></span> |<span data-ttu-id="70b7a-167">계획 되거나 계획 되지 않은 hello 장애 조치는 테스트 하는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-167">Specifies whether hello failover is test, planned, or unplanned.</span></span> |
| <span data-ttu-id="70b7a-168">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="70b7a-168">FailoverDirection</span></span> |<span data-ttu-id="70b7a-169">복구 tooprimary 또는 secondary 상태 인지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-169">Specify whether recovery is tooprimary or secondary</span></span> |
| <span data-ttu-id="70b7a-170">GroupID</span><span class="sxs-lookup"><span data-stu-id="70b7a-170">GroupID</span></span> |<span data-ttu-id="70b7a-171">Hello 계획 실행 중일 때 hello 복구 계획 내에서 hello 그룹 번호를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-171">Identify hello group number within hello recovery plan when hello plan is running</span></span> |
| <span data-ttu-id="70b7a-172">VmMap</span><span class="sxs-lookup"><span data-stu-id="70b7a-172">VmMap</span></span> |<span data-ttu-id="70b7a-173">Hello 그룹의 모든 hello 가상 컴퓨터의 배열</span><span class="sxs-lookup"><span data-stu-id="70b7a-173">Array of all hello virtual machines in hello group</span></span> |
| <span data-ttu-id="70b7a-174">VMMap key</span><span class="sxs-lookup"><span data-stu-id="70b7a-174">VMMap key</span></span> |<span data-ttu-id="70b7a-175">각 VM에 대한 고유 키(GUID)입니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-175">Unique key (GUID) for each VM.</span></span> <span data-ttu-id="70b7a-176">해당 되는 hello 가상 컴퓨터의 VMM ID hello와 같을 hello 했습니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-176">It's hello same as hello VMM ID of hello virtual machine where applicable.</span></span> |
| <span data-ttu-id="70b7a-177">RoleName</span><span class="sxs-lookup"><span data-stu-id="70b7a-177">RoleName</span></span> |<span data-ttu-id="70b7a-178">Hello 복구 되는 Azure VM의 이름</span><span class="sxs-lookup"><span data-stu-id="70b7a-178">Name of hello Azure VM that's being recovered</span></span> |
| <span data-ttu-id="70b7a-179">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="70b7a-179">CloudServiceName</span></span> |<span data-ttu-id="70b7a-180">가상 컴퓨터를 만들 때 어떤 hello에서 azure 클라우드 서비스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-180">Azure Cloud Service name under which hello virtual machine is created.</span></span> |

<span data-ttu-id="70b7a-181">tooidentify hello VmMap 키 hello 컨텍스트에 ASR의 toohello VM 속성 페이지로 이동 하 고 hello VM GUID 속성을 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-181">tooidentify hello VmMap Key in hello context you could also go toohello VM properties page in ASR and look at hello VM GUID property.</span></span>

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a><span data-ttu-id="70b7a-182">자동화 Runbook 작성</span><span class="sxs-lookup"><span data-stu-id="70b7a-182">Author an Automation runbook</span></span>
<span data-ttu-id="70b7a-183">이제 hello 프런트 엔드 가상 컴퓨터에 hello runbook tooopen 포트를 80을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-183">Now create hello runbook tooopen port 80 on hello front-end virtual machine.</span></span>

1. <span data-ttu-id="70b7a-184">Hello hello 이름의 Azure 자동화 계정에서에서 새 runbook을 만들려면 **OpenPort80**</span><span class="sxs-lookup"><span data-stu-id="70b7a-184">Create a new runbook in hello Azure Automation account with hello name **OpenPort80**</span></span>

   ![](media/site-recovery-runbook-automation/14.png)
2. <span data-ttu-id="70b7a-185">Hello runbook의 작성자 보기 toohello 이동한 hello 초안 모드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-185">Navigate toohello Author view of hello runbook and enter hello draft mode.</span></span>
3. <span data-ttu-id="70b7a-186">먼저 hello 변수 toouse hello 복구 계획 컨텍스트로 지정</span><span class="sxs-lookup"><span data-stu-id="70b7a-186">First specify hello variable toouse as hello recovery plan context</span></span>

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. <span data-ttu-id="70b7a-187">그런 다음 toohello 구독 hello 자격 증명 및 구독 이름을 사용 하 여 연결</span><span class="sxs-lookup"><span data-stu-id="70b7a-187">Next connect toohello subscription using hello credential and subscription name</span></span>

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect tooAzure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   <span data-ttu-id="70b7a-188">사용 하는 hello Azure 자산 – **AzureCredential** 및 **AzureSubscriptionName** 여기 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-188">Note that you use hello Azure assets – **AzureCredential** and **AzureSubscriptionName** here.</span></span>
5. <span data-ttu-id="70b7a-189">이제 hello 끝점 세부 정보를 지정 하 고 hello tooexpose hello 끝점을 구하려는 hello 가상 컴퓨터의 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-189">Now specify hello endpoint details and hello GUID of hello virtual machine for which you want tooexpose hello endpoint.</span></span> <span data-ttu-id="70b7a-190">이 사례 hello 프런트 엔드 가상 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-190">In this case hello front-end virtual machine.</span></span>

   ```
       # Specify hello parameters toobe used by hello script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   <span data-ttu-id="70b7a-191">Azure 끝점 프로토콜 hello, hello VM에서 로컬 포트와 해당 매핑된 공용 포트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-191">This specifies hello Azure endpoint protocol, local port on hello VM and its mapped public port.</span></span> <span data-ttu-id="70b7a-192">이러한 변수는 매개 변수 hello에 필요한 끝점 tooVMs 추가 Azure 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-192">These variables are parameters     required by hello Azure commands that add endpoints tooVMs.</span></span> <span data-ttu-id="70b7a-193">hello VMGUID hello에서 toooperate가 필요한 hello 가상 컴퓨터의 GUID를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-193">hello VMGUID holds hello GUID of hello virtual machine you need toooperate on.</span></span>
6. <span data-ttu-id="70b7a-194">hello 스크립트 이제 VM GUID를 지정 하는 hello에 대 한 hello 컨텍스트를 추출 여기에서 참조 하는 hello 가상 컴퓨터에 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-194">hello script will now extract hello context for hello given VM GUID and create an endpoint on hello virtual machine referenced by it.</span></span>

   ```
       #Read hello VM GUID from hello context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke hello necessary pipeline commands tooadd a Azure Endpoint tooa specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. <span data-ttu-id="70b7a-195">이 작업이 완료 되 면 게시 적중 ![](media/site-recovery-runbook-automation/20.png) tooallow 사용자 스크립트 toobe 실행에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-195">Once this is complete, hit Publish ![](media/site-recovery-runbook-automation/20.png) tooallow your script toobe available for execution.</span></span>

<span data-ttu-id="70b7a-196">hello 전체 스크립트는 아래에 지정 된 참조</span><span class="sxs-lookup"><span data-stu-id="70b7a-196">hello complete script is given below for your reference</span></span>

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect tooAzure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify hello parameters toobe used by hello script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read hello VM GUID from hello context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke hello necessary pipeline commands tooadd an Azure Endpoint tooa specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-hello-script-toohello-recovery-plan"></a><span data-ttu-id="70b7a-197">Hello 스크립트 toohello 복구 계획 추가</span><span class="sxs-lookup"><span data-stu-id="70b7a-197">Add hello script toohello recovery plan</span></span>
<span data-ttu-id="70b7a-198">Hello 스크립트 준비 되 면 앞서 만든 toohello 복구 계획을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-198">Once hello script is ready, you can add it toohello recovery plan that you created earlier.</span></span>

1. <span data-ttu-id="70b7a-199">만든 hello 복구 계획 선택 tooadd 스크립트 그룹 2 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-199">In hello recovery plan you created, choose tooadd a script after the group 2.</span></span> ![](media/site-recovery-runbook-automation/15.png)
2. <span data-ttu-id="70b7a-200">스크립트 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-200">Specify a script name.</span></span> <span data-ttu-id="70b7a-201">이 스크립트의 hello 복구 계획 내에서 표시 하기 위한 친숙 한 이름 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-201">This is just a friendly name for this script for showing within hello Recovery plan.</span></span>
3. <span data-ttu-id="70b7a-202">장애 조치 tooAzure 스크립트 hello –에 hello Azure 자동화 계정 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-202">In hello failover tooAzure script – Select hello Azure Automation Account name.</span></span>
4. <span data-ttu-id="70b7a-203">Hello Azure Runbook을 작성 하는 hello runbook을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-203">In hello Azure Runbooks, select hello runbook you authored.</span></span>

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a><span data-ttu-id="70b7a-204">기본 측 스크립트</span><span class="sxs-lookup"><span data-stu-id="70b7a-204">Primary side scripts</span></span>
<span data-ttu-id="70b7a-205">장애 조치 tooAzure를 실행 하는 경우 tooexecute를 기본 측 스크립트도 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-205">When you are executing a failover tooAzure, you can also choose tooexecute primary side scripts.</span></span> <span data-ttu-id="70b7a-206">이러한 스크립트는 장애 조치 중 hello VMM 서버에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-206">These scripts will run on hello VMM server during failover.</span></span>
<span data-ttu-id="70b7a-207">기본 측 스크립트는 종료 전 및 종료 후 단계에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-207">Primary side scripts are only available only for pre-shutdown and post shutdown stages.</span></span> <span data-ttu-id="70b7a-208">B hello 주 사이트 toobe 일반적으로 사용할 수 없는 재해가 발생 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-208">This is because we expect hello primary site toobe typically unavailable when a disaster strikes.</span></span>
<span data-ttu-id="70b7a-209">계획 되지 않은 장애 조치 중에 주 사이트 작업을 위해 선택 하는 경우에 시도 합니다 toorun hello 기본 측 스크립트.</span><span class="sxs-lookup"><span data-stu-id="70b7a-209">During an unplanned failover, only if you opt in for primary site operations, it will attempt toorun hello primary side scripts.</span></span> <span data-ttu-id="70b7a-210">제한 시간 hello 장애 조치는 계속 연결할 수 없는 경우 toorecover hello 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="70b7a-210">If they are not reachable or timeout, hello failover will continue toorecover hello virtual machines.</span></span>
<span data-ttu-id="70b7a-211">기본 측 스크립트 tooAzure 장애 조치 하는 동안 보호 된 VMM tooAzure-없는 VMware/물리적/하이퍼-v 사이트에 사용할 수 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-211">Primary side scripts are un-available for VMware/Physical/Hyper-v Sites without VMM protected tooAzure - while you failover tooAzure.</span></span>
<span data-ttu-id="70b7a-212">그러나 때 장애 복구 Azure tooon 온-프레미스, 기본 측 스크립트 (Runbook)에서 사용할 수 VMware 제외한 모든 대상에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-212">However, when you failback from Azure tooon-premises, primary side scripts (Runbooks) can be used for all targets except VMware.</span></span>

## <a name="test-hello-recovery-plan"></a><span data-ttu-id="70b7a-213">테스트 hello 복구 계획</span><span class="sxs-lookup"><span data-stu-id="70b7a-213">Test hello recovery plan</span></span>
<span data-ttu-id="70b7a-214">Hello runbook toohello 계획을 추가한 후 테스트 장애 조치를 시작 하 고 동작에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-214">Once you have added hello runbook toohello plan you can initiate a test failover and see it in action.</span></span> <span data-ttu-id="70b7a-215">항상 테스트 장애 조치 tootest toorun 권장 프로그램 응용 프로그램 및 hello 복구 계획 tooensure 오류가 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-215">It is always recommended toorun a test failover tootest your application and hello recovery plan tooensure that there are no errors.</span></span>

1. <span data-ttu-id="70b7a-216">Hello 복구 계획을 선택 하 고 테스트 장애 조치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-216">Select hello recovery plan and initiate a test failover.</span></span>
2. <span data-ttu-id="70b7a-217">Hello 계획 실행 중 hello runbook은 실행 여부 또는 통해 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-217">During hello plan execution, you can see whether hello runbook has executed or not via its status.</span></span>

   ![](media/site-recovery-runbook-automation/17.png)
3. <span data-ttu-id="70b7a-218">또한 볼 수 있습니다 hello hello runbook에 대 한 hello Azure 자동화 작업 페이지에서 runbook 실행 상태를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-218">You can also see hello detailed runbook execution status on hello Azure Automation jobs page for hello runbook.</span></span>

   ![](media/site-recovery-runbook-automation/18.png)
4. <span data-ttu-id="70b7a-219">Hello runbook 실행 결과는 별도로 hello 장애 조치가 완료 된 후에 hello 실행이 성공 여부 또는 hello Azure 가상 컴퓨터 페이지를 방문 하 고 hello 끝점을 살펴보면가 아니라를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-219">After hello failover completes, apart from hello runbook execution result, you can see whether hello execution is successful or not by visiting hello Azure virtual machine page and looking at hello endpoints.</span></span>

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a><span data-ttu-id="70b7a-220">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="70b7a-220">Sample scripts</span></span>
<span data-ttu-id="70b7a-221">안내 하는 동안이 자습서에서는 끝점 tooan Azure 가상 컴퓨터를 추가 하는 작업에 사용 되는 일반적으로 하나 자동화, 다양 한 Azure 자동화를 사용 하 여 다른 강력한 자동화 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-221">While we walked through automating one commonly used task of adding an endpoint tooan Azure virtual machine in this tutorial, you could do a number of other powerful automation tasks using Azure automation.</span></span> <span data-ttu-id="70b7a-222">Microsoft 및 hello Azure 자동화 커뮤니티 사용자 고유의 솔루션 및 보다 큰 자동화 작업에 대 한 빌딩 블록으로 사용할 수 있는 유틸리티 runbook을 만들기 전에 수 있는 샘플 runbook을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b7a-222">Microsoft and hello Azure Automation community provide sample runbooks which can help you get started creating your own solutions, and utility runbooks, which you can use as building blocks for larger automation tasks.</span></span> <span data-ttu-id="70b7a-223">Hello 갤러리에서 사용을 시작 하 고 Azure Site Recovery를 사용 하 여 응용 프로그램에 대 한 강력한 한 번의 클릭 복구 계획을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="70b7a-223">Start using them from hello gallery and build  powerful one-click recovery plans for your applications using Azure Site Recovery.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="70b7a-224">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="70b7a-224">Additional Resources</span></span>
[<span data-ttu-id="70b7a-225">Azure 자동화 개요</span><span class="sxs-lookup"><span data-stu-id="70b7a-225">Azure Automation Overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Azure 자동화 개요")

[<span data-ttu-id="70b7a-226">Azure 자동화 스크립트 샘플</span><span class="sxs-lookup"><span data-stu-id="70b7a-226">Sample Azure Automation Scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Azure 자동화 스크립트 샘플")
