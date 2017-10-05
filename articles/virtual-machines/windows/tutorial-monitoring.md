---
title: "Azure 모니터링 및 Windows Virtual Machines | Microsoft Docs"
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
ms.openlocfilehash: 42a475092bdd615c23154e5f813861b0acefcf29
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="7a1ef-103">Azure PowerShell을 사용하여 Windows 가상 컴퓨터 모니터링</span><span class="sxs-lookup"><span data-stu-id="7a1ef-103">Monitor a Windows Virtual Machine with Azure PowerShell</span></span>

<span data-ttu-id="7a1ef-104">Azure 모니터링은 Azure VM에서 부팅 및 성능 데이터를 수집하고, Azure Storage에 이 데이터를 저장하고, 포털, Azure PowerShell 모듈 및 Azure CLI를 통해 액세스할 수 있도록 하는 에이전트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-104">Azure monitoring uses agents to collect boot and performance data from Azure VMs, store this data in Azure storage, and make it accessible through portal, the Azure PowerShell module, and the Azure CLI.</span></span> <span data-ttu-id="7a1ef-105">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7a1ef-106">VM에서 부팅 진단을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="7a1ef-106">Enable boot diagnostics on a VM</span></span>
> * <span data-ttu-id="7a1ef-107">부트 진단 보기</span><span class="sxs-lookup"><span data-stu-id="7a1ef-107">View boot diagnostics</span></span>
> * <span data-ttu-id="7a1ef-108">VM 호스트 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="7a1ef-108">View VM host metrics</span></span>
> * <span data-ttu-id="7a1ef-109">진단 확장 설치</span><span class="sxs-lookup"><span data-stu-id="7a1ef-109">Install the diagnostics extension</span></span>
> * <span data-ttu-id="7a1ef-110">VM 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="7a1ef-110">View VM metrics</span></span>
> * <span data-ttu-id="7a1ef-111">경고 만들기</span><span class="sxs-lookup"><span data-stu-id="7a1ef-111">Create an alert</span></span>
> * <span data-ttu-id="7a1ef-112">고급 모니터링 설정</span><span class="sxs-lookup"><span data-stu-id="7a1ef-112">Set up advanced monitoring</span></span>

<span data-ttu-id="7a1ef-113">이 자습서에는 Azure PowerShell 모듈 버전 3.6 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="7a1ef-114">` Get-Module -ListAvailable AzureRM`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-114">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="7a1ef-115">업그레이드해야 하는 경우 [Azure PowerShell 모듈 설치](/powershell/azure/install-azurerm-ps)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="7a1ef-116">이 자습서의 예제를 완료하려면 기존 가상 컴퓨터가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-116">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="7a1ef-117">필요한 경우 이 [스크립트 샘플](../scripts/virtual-machines-windows-powershell-sample-create-vm.md)을 사용하여 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-117">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="7a1ef-118">자습서를 진행할 때 필요한 경우 리소스 그룹, VM 이름 및 위치를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-118">When working through the tutorial, replace the resource group, VM name, and location where needed.</span></span>

## <a name="view-boot-diagnostics"></a><span data-ttu-id="7a1ef-119">부트 진단 보기</span><span class="sxs-lookup"><span data-stu-id="7a1ef-119">View boot diagnostics</span></span>

<span data-ttu-id="7a1ef-120">Windows 가상 컴퓨터를 부팅하면 부트 진단 에이전트가 문제 해결 목적에 사용할 수 있는 화면 출력을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-120">As Windows virtual machines boot up, the boot diagnostic agent captures screen output that can be used for troubleshooting purpose.</span></span> <span data-ttu-id="7a1ef-121">이 기능은 기본적으로 사용하도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-121">This capability is enabled by default.</span></span> <span data-ttu-id="7a1ef-122">캡처한 스크린샷은 기본적으로 생성되는 Azure Storage 계정에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-122">The captured screen shots are stored in an Azure storage account, which is also created by default.</span></span> 

<span data-ttu-id="7a1ef-123">[Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) 명령으로 부트 진단 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-123">You can get the boot diagnostic data with the [Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) command.</span></span> <span data-ttu-id="7a1ef-124">다음 예제에서는 부트 진단이 *c:\* 드라이브의 루트에 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-124">In the following example, boot diagnostics are downloaded to the root of the *c:\* drive.</span></span> 

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup -Name myVM -Windows -LocalPath "c:\"
```

## <a name="view-host-metrics"></a><span data-ttu-id="7a1ef-125">호스트 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="7a1ef-125">View host metrics</span></span>

<span data-ttu-id="7a1ef-126">Windows VM에는 Azure에서 상호 작용하는 전용 호스트 VM이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-126">A Windows VM has a dedicated Host VM in Azure that it interacts with.</span></span> <span data-ttu-id="7a1ef-127">이 호스트에 대한 메트릭이 자동으로 수집되며, Azure Portal에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-127">Metrics are automatically collected for the Host and can be viewed in the Azure portal.</span></span>

1. <span data-ttu-id="7a1ef-128">Azure Portal에서 **리소스 그룹**을 클릭하고 **myResourceGroup**을 선택한 다음 리소스 목록에서 **myVM**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-128">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
2. <span data-ttu-id="7a1ef-129">호스트 VM이 어떻게 수행되는지 확인하려면 VM 블레이드에서 **메트릭**을 클릭한 다음 **사용 가능한 메트릭**에서 호스트 메트릭 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-129">Click **Metrics** on the VM blade, and then select any of the Host metrics under **Available metrics** to see how the Host VM is performing.</span></span>

    ![호스트 메트릭 보기](./media/tutorial-monitoring/tutorial-monitor-host-metrics.png)

## <a name="install-diagnostics-extension"></a><span data-ttu-id="7a1ef-131">진단 확장 설치</span><span class="sxs-lookup"><span data-stu-id="7a1ef-131">Install diagnostics extension</span></span>

<span data-ttu-id="7a1ef-132">기본 호스트 메트릭을 사용할 수 있지만, 더 세분화된 VM 관련 메트릭을 보려면 VM에 Azure 진단 확장을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-132">The basic host metrics are available, but to see more granular and VM-specific metrics, you to need to install the Azure diagnostics extension on the VM.</span></span> <span data-ttu-id="7a1ef-133">Azure 진단 확장을 사용하면 VM에서 추가 모니터링 및 진단 데이터를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-133">The Azure diagnostics extension allows additional monitoring and diagnostics data to be retrieved from the VM.</span></span> <span data-ttu-id="7a1ef-134">이러한 성능 메트릭을 보고 VM 성능에 따라 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-134">You can view these performance metrics and create alerts based on how the VM performs.</span></span> <span data-ttu-id="7a1ef-135">진단 확장은 다음과 같이 Azure Portal을 통해 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-135">The diagnostic extension is installed through the Azure portal as follows:</span></span>

1. <span data-ttu-id="7a1ef-136">Azure Portal에서 **리소스 그룹**을 클릭하고 **myResourceGroup**을 선택한 다음 리소스 목록에서 **myVM**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-136">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
2. <span data-ttu-id="7a1ef-137">**진단 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-137">Click **Diagnosis settings**.</span></span> <span data-ttu-id="7a1ef-138">목록에서는 *부트 진단*이 이전 섹션에서 이미 사용하도록 설정되었음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-138">The list shows that *Boot diagnostics* are already enabled from the previous section.</span></span> <span data-ttu-id="7a1ef-139">*기본 메트릭*에 대한 확인란을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-139">Click the check box for *Basic metrics*.</span></span>
3. <span data-ttu-id="7a1ef-140">**게스트 수준 모니터링을 사용하도록 설정** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-140">Click the **Enable guest-level monitoring** button.</span></span>

    ![진단 메트릭 보기](./media/tutorial-monitoring/enable-diagnostics-extension.png)

## <a name="view-vm-metrics"></a><span data-ttu-id="7a1ef-142">VM 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="7a1ef-142">View VM metrics</span></span>

<span data-ttu-id="7a1ef-143">호스트 VM 메트릭을 본 것과 동일한 방법으로 VM 메트릭을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-143">You can view the VM metrics in the same way that you viewed the host VM metrics:</span></span>

1. <span data-ttu-id="7a1ef-144">Azure Portal에서 **리소스 그룹**을 클릭하고 **myResourceGroup**을 선택한 다음 리소스 목록에서 **myVM**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-144">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
2. <span data-ttu-id="7a1ef-145">VM의 성능을 보려면 VM 블레이드에서 **메트릭**을 클릭한 다음 **사용 가능한 메트릭**에서 진단 메트릭 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-145">To see how the VM is performing, click **Metrics** on the VM blade, and then select any of the diagnostics metrics under **Available metrics**.</span></span>

    ![VM 메트릭 보기](./media/tutorial-monitoring/monitor-vm-metrics.png)

## <a name="create-alerts"></a><span data-ttu-id="7a1ef-147">경고 만들기</span><span class="sxs-lookup"><span data-stu-id="7a1ef-147">Create alerts</span></span>

<span data-ttu-id="7a1ef-148">특정 성능 메트릭을 기반으로 하는 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-148">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="7a1ef-149">예를 들어 평균 CPU 사용량이 특정 임계값을 초과하거나 사용 가능한 디스크 공간이 일정량 이하로 떨어지면 경고를 사용하여 사용자에게 알릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-149">Alerts can be used to notify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="7a1ef-150">경고는 Azure Portal에 표시되거나 전자 메일을 통해 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-150">Alerts are displayed in the Azure portal or can be sent via email.</span></span> <span data-ttu-id="7a1ef-151">또한 생성되는 경고에 대한 응답으로 Azure Automation Runbook 또는 Azure Logic Apps를 트리거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-151">You can also trigger Azure Automation runbooks or Azure Logic Apps in response to alerts being generated.</span></span>

<span data-ttu-id="7a1ef-152">다음 예제에서는 평균 CPU 사용량에 대한 경고를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-152">The following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="7a1ef-153">Azure Portal에서 **리소스 그룹**을 클릭하고 **myResourceGroup**을 선택한 다음 리소스 목록에서 **myVM**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-153">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
2. <span data-ttu-id="7a1ef-154">VM 블레이드에서 **경고 규칙**을 클릭한 다음, 경고 블레이드 위쪽에 있는 **메트릭 경고 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-154">Click **Alert rules** on the VM blade, then click **Add metric alert** across the top of the alerts blade.</span></span>
4. <span data-ttu-id="7a1ef-155">*myAlertRule*과 같이 경고에 대한 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-155">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="7a1ef-156">CPU 사용률이 5분 동안 1.0을 초과할 때 경고를 트리거하려면 다른 모든 기본값을 선택한 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-156">To trigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all the other defaults selected.</span></span>
6. <span data-ttu-id="7a1ef-157">필요한 경우 전자 메일 알림을 보내도록 *전자 메일 소유자, 참가자 및 읽기 권한자*의 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-157">Optionally, check the box for *Email owners, contributors, and readers* to send email notification.</span></span> <span data-ttu-id="7a1ef-158">기본 작업은 포털에서 알림을 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-158">The default action is to present a notification in the portal.</span></span>
7. <span data-ttu-id="7a1ef-159">**확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-159">Click the **OK** button.</span></span>

## <a name="advanced-monitoring"></a><span data-ttu-id="7a1ef-160">고급 모니터링</span><span class="sxs-lookup"><span data-stu-id="7a1ef-160">Advanced monitoring</span></span> 

<span data-ttu-id="7a1ef-161">[Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)를 사용하여 VM에 대한 고급 모니터링을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-161">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="7a1ef-162">아직 사용해 보지 않았으면 Operations Management Suite의 [평가판](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-162">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="7a1ef-163">OMS 포털에 액세스할 수 있으면 설정 블레이드에서 작업 영역 키와 작업 영역 식별자를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-163">When you have access to the OMS portal, you can find the workspace key and workspace identifier on the Settings blade.</span></span> <span data-ttu-id="7a1ef-164">[Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) 명령을 사용하여 OMS 확장을 VM에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-164">Use the [Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) cmmand to to add the OMS extension to the VM.</span></span> <span data-ttu-id="7a1ef-165">아래 샘플에서는 변수 값을 업데이트하여 OMS 작업 영역 키 및 작업 영역 ID를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-165">Update the variable values in the below sample to reflect you OMS workspace key and workspace Id.</span></span>  

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

<span data-ttu-id="7a1ef-166">몇 분 후 새 VM이 OMS 작업 영역에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-166">After a few minutes, you should see the new VM in the OMS workspace.</span></span> 

![OMS 블레이드](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="7a1ef-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7a1ef-168">Next steps</span></span>
<span data-ttu-id="7a1ef-169">이 자습서에서는 Azure Security Center를 사용하여 VM을 구성하고 검토했습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-169">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="7a1ef-170">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-170">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7a1ef-171">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="7a1ef-171">Create a virtual network</span></span>
> * <span data-ttu-id="7a1ef-172">리소스 그룹 및 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="7a1ef-172">Create a resource group and VM</span></span> 
> * <span data-ttu-id="7a1ef-173">VM에서 부트 진단을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="7a1ef-173">Enable boot diagnostics on the VM</span></span>
> * <span data-ttu-id="7a1ef-174">부트 진단 보기</span><span class="sxs-lookup"><span data-stu-id="7a1ef-174">View boot diagnostics</span></span>
> * <span data-ttu-id="7a1ef-175">호스트 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="7a1ef-175">View host metrics</span></span>
> * <span data-ttu-id="7a1ef-176">진단 확장 설치</span><span class="sxs-lookup"><span data-stu-id="7a1ef-176">Install the diagnostics extension</span></span>
> * <span data-ttu-id="7a1ef-177">VM 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="7a1ef-177">View VM metrics</span></span>
> * <span data-ttu-id="7a1ef-178">경고 만들기</span><span class="sxs-lookup"><span data-stu-id="7a1ef-178">Create an alert</span></span>
> * <span data-ttu-id="7a1ef-179">고급 모니터링 설정</span><span class="sxs-lookup"><span data-stu-id="7a1ef-179">Set up advanced monitoring</span></span>

<span data-ttu-id="7a1ef-180">Azure Security Center에 대해 알아보려면 다음 자습서로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1ef-180">Advance to the next tutorial to learn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7a1ef-181">VM 보안 관리</span><span class="sxs-lookup"><span data-stu-id="7a1ef-181">Manage VM security</span></span>](./tutorial-azure-security.md)