---
title: "aaaAzure 모니터링 및 Windows 가상 컴퓨터 | Microsoft Docs"
description: "자습서 - Azure PowerShell을 사용하여 Windows 가상 컴퓨터 모니터링"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/04/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 191dc5a30d41c25a9e38f8ec2a32efdc05e03015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="3e96a-103">Azure PowerShell을 사용하여 Windows 가상 컴퓨터 모니터링</span><span class="sxs-lookup"><span data-stu-id="3e96a-103">Monitor a Windows Virtual Machine with Azure PowerShell</span></span>

<span data-ttu-id="3e96a-104">Azure 모니터링 에이전트 toocollect 부팅을 사용 하 고 Azure Vm의 성능 데이터를 Azure 저장소에이 데이터를 저장 하 고 포털, hello Azure PowerShell 모듈 및 hello Azure CLI를 통해 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-104">Azure monitoring uses agents toocollect boot and performance data from Azure VMs, store this data in Azure storage, and make it accessible through portal, hello Azure PowerShell module, and hello Azure CLI.</span></span> <span data-ttu-id="3e96a-105">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3e96a-106">VM에서 부팅 진단을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="3e96a-106">Enable boot diagnostics on a VM</span></span>
> * <span data-ttu-id="3e96a-107">부트 진단 보기</span><span class="sxs-lookup"><span data-stu-id="3e96a-107">View boot diagnostics</span></span>
> * <span data-ttu-id="3e96a-108">VM 호스트 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="3e96a-108">View VM host metrics</span></span>
> * <span data-ttu-id="3e96a-109">Hello 진단 확장을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-109">Install hello diagnostics extension</span></span>
> * <span data-ttu-id="3e96a-110">VM 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="3e96a-110">View VM metrics</span></span>
> * <span data-ttu-id="3e96a-111">경고 만들기</span><span class="sxs-lookup"><span data-stu-id="3e96a-111">Create an alert</span></span>
> * <span data-ttu-id="3e96a-112">고급 모니터링 설정</span><span class="sxs-lookup"><span data-stu-id="3e96a-112">Set up advanced monitoring</span></span>

<span data-ttu-id="3e96a-113">이 자습서는 Azure PowerShell 모듈 버전 3.6 이상 hello가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="3e96a-114">실행 ` Get-Module -ListAvailable AzureRM` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="3e96a-115">Tooupgrade 필요한 경우 참조 [Azure PowerShell 설치 모듈](/powershell/azure/install-azurerm-ps)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="3e96a-116">이 자습서에서는 toocomplete hello 예제에서는 기존 가상 컴퓨터 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-116">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="3e96a-117">필요한 경우 이 [스크립트 샘플](../scripts/virtual-machines-windows-powershell-sample-create-vm.md)을 사용하여 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-117">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="3e96a-118">Hello 자습서를 살펴보면서 hello 리소스 그룹, VM 이름 및 위치 대체 필요한 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-118">When working through hello tutorial, replace hello resource group, VM name, and location where needed.</span></span>

## <a name="view-boot-diagnostics"></a><span data-ttu-id="3e96a-119">부트 진단 보기</span><span class="sxs-lookup"><span data-stu-id="3e96a-119">View boot diagnostics</span></span>

<span data-ttu-id="3e96a-120">Windows 가상 컴퓨터를 부팅 하는 대로 hello 부트 진단 에이전트 문제 해결 목적으로 사용할 수 있는 화면 출력을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-120">As Windows virtual machines boot up, hello boot diagnostic agent captures screen output that can be used for troubleshooting purpose.</span></span> <span data-ttu-id="3e96a-121">이 기능은 기본적으로 사용하도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-121">This capability is enabled by default.</span></span> <span data-ttu-id="3e96a-122">hello 캡처한 스크린 샷 함께 기본적으로 생성 되는 Azure 저장소 계정에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-122">hello captured screen shots are stored in an Azure storage account, which is also created by default.</span></span> 

<span data-ttu-id="3e96a-123">Hello 사용 하 여 hello 부트 진단 데이터를 가져올 수 있습니다 [Get AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-123">You can get hello boot diagnostic data with hello [Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) command.</span></span> <span data-ttu-id="3e96a-124">다음 예제는 hello, 부트 진단이는 hello의 다운로드 한 toohello 루트 * c:\* 드라이브입니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-124">In hello following example, boot diagnostics are downloaded toohello root of hello *c:\* drive.</span></span> 

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup -Name myVM -Windows -LocalPath "c:\"
```

## <a name="view-host-metrics"></a><span data-ttu-id="3e96a-125">호스트 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="3e96a-125">View host metrics</span></span>

<span data-ttu-id="3e96a-126">Windows VM에는 Azure에서 상호 작용하는 전용 호스트 VM이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-126">A Windows VM has a dedicated Host VM in Azure that it interacts with.</span></span> <span data-ttu-id="3e96a-127">메트릭은 호스트 hello에 대 한 자동으로 수집 되며 hello Azure 포털에서에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-127">Metrics are automatically collected for hello Host and can be viewed in hello Azure portal.</span></span>

1. <span data-ttu-id="3e96a-128">Hello Azure 포털에서에서 클릭 **리소스 그룹**선택, **myResourceGroup**를 선택한 후 **myVM** hello 리소스 목록에 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-128">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="3e96a-129">클릭 **메트릭** VM 블레이드 hello 되 고 아래 hello 호스트 메트릭 중 하나를 선택 **사용 가능한 메트릭** toosee hello 호스트 VM 수행 방법.</span><span class="sxs-lookup"><span data-stu-id="3e96a-129">Click **Metrics** on hello VM blade, and then select any of hello Host metrics under **Available metrics** toosee how hello Host VM is performing.</span></span>

    ![호스트 메트릭 보기](./media/tutorial-monitoring/tutorial-monitor-host-metrics.png)

## <a name="install-diagnostics-extension"></a><span data-ttu-id="3e96a-131">진단 확장 설치</span><span class="sxs-lookup"><span data-stu-id="3e96a-131">Install diagnostics extension</span></span>

<span data-ttu-id="3e96a-132">hello 기본 호스트 메트릭을 사용할 수 있는 보다 세부적인 toosee 있고 VM 관련 메트릭, 있습니다 tooneed tooinstall hello Azure 진단 확장을 hello VM입니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-132">hello basic host metrics are available, but toosee more granular and VM-specific metrics, you tooneed tooinstall hello Azure diagnostics extension on hello VM.</span></span> <span data-ttu-id="3e96a-133">hello Azure 진단 확장 추가 모니터링 및 진단 데이터 toobe hello VM에서에서 검색을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-133">hello Azure diagnostics extension allows additional monitoring and diagnostics data toobe retrieved from hello VM.</span></span> <span data-ttu-id="3e96a-134">이러한 성능 메트릭을 보고 하 고 hello VM 수행 하는 방법을 기반으로 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-134">You can view these performance metrics and create alerts based on how hello VM performs.</span></span> <span data-ttu-id="3e96a-135">hello 진단 확장 다음과 같이 hello Azure 포털을 통해 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-135">hello diagnostic extension is installed through hello Azure portal as follows:</span></span>

1. <span data-ttu-id="3e96a-136">Hello Azure 포털에서에서 클릭 **리소스 그룹**선택, **myResourceGroup**를 선택한 후 **myVM** hello 리소스 목록에 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-136">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="3e96a-137">**진단 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-137">Click **Diagnosis settings**.</span></span> <span data-ttu-id="3e96a-138">hello 목록에 표시 하는 *진단 부팅* hello 이전 단원에서 이미 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-138">hello list shows that *Boot diagnostics* are already enabled from hello previous section.</span></span> <span data-ttu-id="3e96a-139">Hello에 대 한 확인란을 클릭 *기본 메트릭*합니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-139">Click hello check box for *Basic metrics*.</span></span>
3. <span data-ttu-id="3e96a-140">Hello 클릭 **게스트 수준 모니터링 사용** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-140">Click hello **Enable guest-level monitoring** button.</span></span>

    ![진단 메트릭 보기](./media/tutorial-monitoring/enable-diagnostics-extension.png)

## <a name="view-vm-metrics"></a><span data-ttu-id="3e96a-142">VM 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="3e96a-142">View VM metrics</span></span>

<span data-ttu-id="3e96a-143">Hello hello VM 메트릭을 볼 수 있습니다 동일한 방식으로 hello 호스트 VM 메트릭을 보았습니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-143">You can view hello VM metrics in hello same way that you viewed hello host VM metrics:</span></span>

1. <span data-ttu-id="3e96a-144">Hello Azure 포털에서에서 클릭 **리소스 그룹**선택, **myResourceGroup**를 선택한 후 **myVM** hello 리소스 목록에 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-144">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="3e96a-145">toosee hello VM을 수행 하는 방법을 클릭 **메트릭** VM 블레이드 hello 되 고 아래 hello 진단 메트릭 중 하나를 선택 **사용 가능한 메트릭**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-145">toosee how hello VM is performing, click **Metrics** on hello VM blade, and then select any of hello diagnostics metrics under **Available metrics**.</span></span>

    ![VM 메트릭 보기](./media/tutorial-monitoring/monitor-vm-metrics.png)

## <a name="create-alerts"></a><span data-ttu-id="3e96a-147">경고 만들기</span><span class="sxs-lookup"><span data-stu-id="3e96a-147">Create alerts</span></span>

<span data-ttu-id="3e96a-148">특정 성능 메트릭을 기반으로 하는 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-148">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="3e96a-149">경고에는 예를 들어 사용된 toonotify 평균 CPU 사용률이 특정 임계값 또는 사용 가능한 디스크 공간을 초과 하는 일정량 아래로 떨어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-149">Alerts can be used toonotify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="3e96a-150">경고나 hello Azure 포털에에서 표시 되는 전자 메일을 통해 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-150">Alerts are displayed in hello Azure portal or can be sent via email.</span></span> <span data-ttu-id="3e96a-151">또한 Azure 자동화 runbook 또는 Azure 논리 앱에서 생성 되 고 응답 tooalerts 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-151">You can also trigger Azure Automation runbooks or Azure Logic Apps in response tooalerts being generated.</span></span>

<span data-ttu-id="3e96a-152">hello 다음 예제에서는 평균 CPU 사용량에 대 한 경고</span><span class="sxs-lookup"><span data-stu-id="3e96a-152">hello following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="3e96a-153">Hello Azure 포털에서에서 클릭 **리소스 그룹**선택, **myResourceGroup**를 선택한 후 **myVM** hello 리소스 목록에 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-153">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="3e96a-154">클릭 **규칙 경고** hello VM 블레이드에서 클릭 **추가 메트릭 경고** hello 경고 블레이드의 hello 위쪽 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-154">Click **Alert rules** on hello VM blade, then click **Add metric alert** across hello top of hello alerts blade.</span></span>
4. <span data-ttu-id="3e96a-155">*myAlertRule*과 같이 경고에 대한 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-155">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="3e96a-156">tootrigger CPU 백분율을 5 분 동안 1.0을 초과할 때 경고 모든 hello 선택한 다른 기본값을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-156">tootrigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all hello other defaults selected.</span></span>
6. <span data-ttu-id="3e96a-157">필요에 따라 확인란 hello에 대 한 *소유자, 참가자 및 독자를 전자 메일로 보내기* toosend 전자 메일 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-157">Optionally, check hello box for *Email owners, contributors, and readers* toosend email notification.</span></span> <span data-ttu-id="3e96a-158">hello 기본 동작은 toopresent hello 포털의 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-158">hello default action is toopresent a notification in hello portal.</span></span>
7. <span data-ttu-id="3e96a-159">Hello 클릭 **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-159">Click hello **OK** button.</span></span>

## <a name="advanced-monitoring"></a><span data-ttu-id="3e96a-160">고급 모니터링</span><span class="sxs-lookup"><span data-stu-id="3e96a-160">Advanced monitoring</span></span> 

<span data-ttu-id="3e96a-161">[Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)를 사용하여 VM에 대한 고급 모니터링을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-161">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="3e96a-162">아직 사용해 보지 않았으면 Operations Management Suite의 [평가판](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-162">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="3e96a-163">액세스 toohello OMS 포털을 사용 하는 경우에 hello 설정 블레이드에서 hello 작업 영역 키 및 작업 영역 id를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-163">When you have access toohello OMS portal, you can find hello workspace key and workspace identifier on hello Settings blade.</span></span> <span data-ttu-id="3e96a-164">사용 하 여 hello [집합 AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) 심에 tootooadd hello OMS 확장 toohello VM입니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-164">Use hello [Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) cmmand tootooadd hello OMS extension toohello VM.</span></span> <span data-ttu-id="3e96a-165">업데이트 hello 변수 값에 샘플 tooreflect 아래 hello 하면 OMS 작업 영역 키 및 작업 영역 id입니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-165">Update hello variable values in hello below sample tooreflect you OMS workspace key and workspace Id.</span></span>  

```powershell
$omsId = "<Replace with your OMS Id>"
$omsKey = "<Replace with your OMS key>"

Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
  -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
  -VMName myVM `
  -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
  -ExtensionType "MicrosoftMonitoringAgent" `
  -TypeHandlerVersion 1.0 `
  -Settings @{"workspaceId" = $omsId} `
  -ProtectedSettings @{"workspaceKey" = $omsKey} `
  -Location eastus
```

<span data-ttu-id="3e96a-166">몇 분 후 나타납니다 hello OMS 작업 영역에서 새 VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-166">After a few minutes, you should see hello new VM in hello OMS workspace.</span></span> 

![OMS 블레이드](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="3e96a-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3e96a-168">Next steps</span></span>
<span data-ttu-id="3e96a-169">이 자습서에서는 Azure Security Center를 사용하여 VM을 구성하고 검토했습니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-169">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="3e96a-170">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-170">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3e96a-171">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="3e96a-171">Create a virtual network</span></span>
> * <span data-ttu-id="3e96a-172">리소스 그룹 및 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="3e96a-172">Create a resource group and VM</span></span> 
> * <span data-ttu-id="3e96a-173">Hello VM에 대 한 부트 진단 유틸리티를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="3e96a-173">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="3e96a-174">부트 진단 보기</span><span class="sxs-lookup"><span data-stu-id="3e96a-174">View boot diagnostics</span></span>
> * <span data-ttu-id="3e96a-175">호스트 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="3e96a-175">View host metrics</span></span>
> * <span data-ttu-id="3e96a-176">Hello 진단 확장을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-176">Install hello diagnostics extension</span></span>
> * <span data-ttu-id="3e96a-177">VM 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="3e96a-177">View VM metrics</span></span>
> * <span data-ttu-id="3e96a-178">경고 만들기</span><span class="sxs-lookup"><span data-stu-id="3e96a-178">Create an alert</span></span>
> * <span data-ttu-id="3e96a-179">고급 모니터링 설정</span><span class="sxs-lookup"><span data-stu-id="3e96a-179">Set up advanced monitoring</span></span>

<span data-ttu-id="3e96a-180">Azure 보안 센터에 대 한 다음 자습서 toolearn toohello를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e96a-180">Advance toohello next tutorial toolearn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3e96a-181">VM 보안 관리</span><span class="sxs-lookup"><span data-stu-id="3e96a-181">Manage VM security</span></span>](./tutorial-azure-security.md)