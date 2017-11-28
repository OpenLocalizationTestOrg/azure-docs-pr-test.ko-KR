---
title: "Azure PowerShell을 사용하여 Windows VM에서 진단을 사용하도록 설정 | Microsoft Docs"
services: virtual-machines-windows
documentationcenter: 
description: "PowerShell을 사용하여 Windows를 실행하는 가상 컴퓨터에서 Azure 진단을 사용하도록 설정하는 방법에 대해 알아봅니다."
author: sbtron
manager: timlt
editor: 
ms.assetid: 2e6d88f2-1980-4a24-827e-a81616a0d247
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: saurabh
ms.openlocfilehash: d0be4a712657edfc516c5f32e66519f5d9486728
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-enable-azure-diagnostics-in-a-virtual-machine-running-windows"></a><span data-ttu-id="5d9f1-103">PowerShell을 사용하여 Windows를 실행하는 가상 컴퓨터에서 Azure 진단을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="5d9f1-103">Use PowerShell to enable Azure Diagnostics in a virtual machine running Windows</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="5d9f1-104">Azure 진단은 배포된 응용 프로그램에서 진단 데이터를 수집할 수 있도록 하는 Azure 내 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-104">Azure Diagnostics is the capability within Azure that enables the collection of diagnostic data on a deployed application.</span></span> <span data-ttu-id="5d9f1-105">진단 확장을 사용하여 Windows를 실행 중인 Azure 가상 컴퓨터(VM)에서 응용 프로그램 로그 또는 성능 카운터 등과 같은 진단 데이터를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-105">You can use the diagnostics extension to collect diagnostic data like application logs or performance counters from an Azure virtual machine (VM) that is running Windows.</span></span> <span data-ttu-id="5d9f1-106">이 문서는 Windows PowerShell을 사용하여 VM에 대해 진단 확장을 사용하도록 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-106">This article describes how to use Windows PowerShell to enable the diagnostics extension for a VM.</span></span> <span data-ttu-id="5d9f1-107">이 문서에 요구되는 필수 조건은 [Azure PowerShell 설치 및 구성하는 방법](/powershell/azure/overview) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-107">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span>

## <a name="enable-the-diagnostics-extension-if-you-use-the-resource-manager-deployment-model"></a><span data-ttu-id="5d9f1-108">리소스 관리자 배포 모델을 사용하는 경우 진단 확장을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="5d9f1-108">Enable the diagnostics extension if you use the Resource Manager deployment model</span></span>
<span data-ttu-id="5d9f1-109">Azure 리소스 관리자 배포 모델을 통해 Windows VM을 만드는 동안 리소스 관리자 템플릿에 확장 구성을 추가하여 진단 확장을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-109">You can enable the diagnostics extension while you create a Windows VM through the Azure Resource Manager deployment model by adding the extension configuration to the Resource Manager template.</span></span> <span data-ttu-id="5d9f1-110">[Azure Resource Manager를 사용하여 Windows 가상 컴퓨터와 모니터링 및 진단 기능 만들기](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-110">See [Create a Windows virtual machine with monitoring and diagnostics by using the Azure Resource Manager template](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="5d9f1-111">리소스 관리자 배포 모델을 통해 만든 기존 VM에서 진단 확장을 사용하도록 설정하려면 아래 표시된 [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) PowerShell cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-111">To enable the diagnostics extension on an existing VM that was created through the Resource Manager deployment model, you can use the [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) PowerShell cmdlet as shown below.</span></span>

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


<span data-ttu-id="5d9f1-112">*$diagnosticsconfig_path*는 아래 [샘플](#sample-diagnostics-configuration)에 설명된 XML의 진단 구성이 포함된 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-112">*$diagnosticsconfig_path* is the path to the file that contains the diagnostics configuration in XML, as described in the [sample](#sample-diagnostics-configuration) below.</span></span>  

<span data-ttu-id="5d9f1-113">진단 구성 파일이 저장소 계정 이름으로 **StorageAccount** 요소를 지정할 경우 *Set-AzureRMVMDiagnosticsExtension* 스크립트에서 해당 저장소 계정으로 진단 데이터를 보내도록 진단 확장을 자동으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-113">If the diagnostics configuration file specifies a **StorageAccount** element with a storage account name, then the *Set-AzureRMVMDiagnosticsExtension* script will automatically set the diagnostics extension to send diagnostic data to that storage account.</span></span> <span data-ttu-id="5d9f1-114">이렇게 작동하려면, 저장소 계정이 VM과 동일한 구독 내에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-114">For this to work, the storage account needs to be in the same subscription as the VM.</span></span>

<span data-ttu-id="5d9f1-115">진단 구성에 **StorageAccount** 가 지정되지 않은 경우 cmdlet에 *StorageAccountName* 매개 변수를 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-115">If no **StorageAccount** was specified in the diagnostics configuration, then you need to pass in the *StorageAccountName* parameter to the cmdlet.</span></span> <span data-ttu-id="5d9f1-116">*StorageAccountName* 매개 변수가 지정된 경우 cmdlet은 항상 진단 구성 파일에 지정된 저장소 계정이 아닌 매개 변수에 지정된 저장소 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-116">If the *StorageAccountName* parameter is specified, then the cmdlet will always use the storage account that is specified in the parameter and not the one that is specified in the diagnostics configuration file.</span></span>

<span data-ttu-id="5d9f1-117">진단 저장소 계정이 VM과 다른 구독에 있는 경우 *StorageAccountName* 및 *StorageAccountKey* 매개 변수를 cmdlet에 명시적으로 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-117">If the diagnostics storage account is in a different subscription from the VM, then you need to explicitly pass in the *StorageAccountName* and *StorageAccountKey* parameters to the cmdlet.</span></span> <span data-ttu-id="5d9f1-118">진단 저장소 계정이 동일한 구독에 있는 경우 진단 확장을 사용하도록 설정하면 cmdlet이 키 값을 자동으로 쿼리하고 설정할 수 있으므로 *StorageAccountKey* 매개 변수가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-118">The *StorageAccountKey* parameter is not needed when the diagnostics storage account is in the same subscription, as the cmdlet can automatically query and set the key value when enabling the diagnostics extension.</span></span> <span data-ttu-id="5d9f1-119">하지만 진단 저장소 계정이 다른 구독에 있는 경우에는 cmdlet이 자동으로 키를 얻지 못할 수 있으며, 사용자가 *StorageAccountKey* 매개 변수를 통해 키를 명시적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-119">However, if the diagnostics storage account is in a different subscription, then the cmdlet might not be able to get the key automatically and you need to explicitly specify the key through the *StorageAccountKey* parameter.</span></span>  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

<span data-ttu-id="5d9f1-120">VM에서 진단 확장을 사용하도록 설정하면 [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet을 사용하여 현재 설정을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-120">Once the diagnostics extension is enabled on a VM, you can get the current settings by using the [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.</span></span>

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

<span data-ttu-id="5d9f1-121">cmdlet은 *PublicSettings*를 반환하며, 여기에는 진단 구성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-121">The cmdlet returns *PublicSettings*, which contains the diagnostics configuration.</span></span> <span data-ttu-id="5d9f1-122">WadCfg 및 xmlCfg의 두 종류의 구성이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-122">There are two kinds of configuration supported, WadCfg and xmlCfg.</span></span> <span data-ttu-id="5d9f1-123">WadCfg는 JSON 구성이며 xmlCfg는 Base64 인코딩 형식의 XML 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-123">WadCfg is JSON configuration, and xmlCfg is XML configuration in a Base64-encoded format.</span></span> <span data-ttu-id="5d9f1-124">XML을 읽으려면 디코딩해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-124">To read the XML, you need to decode it.</span></span>

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

<span data-ttu-id="5d9f1-125">[Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet을 사용하면 VM에서 진단 확장을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-125">The [Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet can be used to remove the diagnostics extension from the VM.</span></span>  

## <a name="enable-the-diagnostics-extension-if-you-use-the-classic-deployment-model"></a><span data-ttu-id="5d9f1-126">클래식 배포 모델을 사용하는 경우 진단 확장을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="5d9f1-126">Enable the diagnostics extension if you use the classic deployment model</span></span>
<span data-ttu-id="5d9f1-127">[Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet을 사용하면 클래식 배포 모델을 통해 만든 VM에서 진단 확장을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-127">You can use the [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet to enable a diagnostics extension on a VM that you create through the classic deployment model.</span></span> <span data-ttu-id="5d9f1-128">다음 예제에서는 클래식 배포 모델을 통해 새 VM을 만들고 진단 확장을 사용하도록 설정하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-128">The following example shows how to create a new VM through the classic deployment model with the diagnostics extension enabled.</span></span>

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

<span data-ttu-id="5d9f1-129">클래식 배포 모델을 통해 만든 기존 VM에서 진단 확장을 사용하도록 설정하려면, 우선 [Get-AzureVM](/powershell/module/azure/get-azurevm) cmdlet을 사용하여 VM 구성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-129">To enable the diagnostics extension on an existing VM that was created through the classic deployment model, first use the [Get-AzureVM](/powershell/module/azure/get-azurevm) cmdlet to get the VM configuration.</span></span> <span data-ttu-id="5d9f1-130">그런 다음 [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet을 사용하여 진단 확장을 포함하도록 VM 구성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-130">Then update the VM configuration to include the diagnostics extension by using the [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet.</span></span> <span data-ttu-id="5d9f1-131">마지막으로 [Update-AzureVM](/powershell/module/azure/update-azurevm)을 사용하여 VM에 업데이트된 구성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-131">Finally, apply the updated configuration to the VM by using [Update-AzureVM](/powershell/module/azure/update-azurevm).</span></span>

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a><span data-ttu-id="5d9f1-132">샘플 진단 구성</span><span class="sxs-lookup"><span data-stu-id="5d9f1-132">Sample diagnostics configuration</span></span>
<span data-ttu-id="5d9f1-133">위의 스크립트를 통해 진단 공용 구성에 다음과 같은 XML을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-133">The following XML can be used for the diagnostics public configuration with the above scripts.</span></span> <span data-ttu-id="5d9f1-134">이 샘플 구성은 Windows 이벤트 로그의 응용 프로그램, 보안 및 시스템 채널 오류 및 진단 인프라 로그의 오류와 함께 다양한 성능 카운터를 저장소 계정으로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-134">This sample configuration will transfer various performance counters to the diagnostics storage account, along with errors from the application, security, and system channels in the Windows event logs and any errors from the diagnostics infrastructure logs.</span></span>

<span data-ttu-id="5d9f1-135">다음을 포함하도록 구성을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-135">The configuration needs to be updated to include the following:</span></span>

* <span data-ttu-id="5d9f1-136">*Metrics* 요소의 **resourceID** 특성을 VM의 리소스 ID로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-136">The *resourceID* attribute of the **Metrics** element needs to be updated with the resource ID for the VM.</span></span>
  
  * <span data-ttu-id="5d9f1-137">리소스 ID는 "/subscriptions/{*VM과 관련된 구독의 구독 ID*}/resourceGroups/{*VM의 리소스 그룹 이름*}/providers/Microsoft.Compute/virtualMachines/{*VM 이름*}"과 같은 패턴을 사용하여 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-137">The resource ID can be constructed by using the following pattern: "/subscriptions/{*subscription ID for the subscription with the VM*}/resourceGroups/{*The resourcegroup name for the VM*}/providers/Microsoft.Compute/virtualMachines/{*The VM Name*}".</span></span>
  * <span data-ttu-id="5d9f1-138">예를 들어 VM이 실행 중인 구독의 구독 ID가 **11111111-1111-1111-1111-111111111111**이고, 리소스 그룹의 리소스 그룹 이름이 **MyResourceGroup**이고, VM 이름이 **MyWindowsVM**일 경우 *resourceID* 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-138">For example, if the subscription ID for the subscription where the VM is running is **11111111-1111-1111-1111-111111111111**, the resource group name for the resource group is **MyResourceGroup**, and the VM Name is **MyWindowsVM**, then the value for *resourceID* would be:</span></span>
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * <span data-ttu-id="5d9f1-139">성능 카운터와 메트릭 구성을 기반으로 메트릭을 생성하는 방법에 대한 자세한 내용은 [Azure Diagnostics metrics table in storage(저장소의 Azure 진단 메트릭 테이블)](extensions-diagnostics-template.md#wadmetrics-tables-in-storage)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-139">For more information on how metrics are generated based on the performance counters and metrics configuration, see [Azure Diagnostics metrics table in storage](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span></span>
* <span data-ttu-id="5d9f1-140">**StorageAccount** 요소를 진단 저장소 계정의 이름으로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-140">The **StorageAccount** element needs to be updated with the name of the diagnostics storage account.</span></span>
  
    ```
    <?xml version="1.0" encoding="utf-8"?>
    <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
        <WadCfg>
          <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
            <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error"/>
            <PerformanceCounters scheduledTransferPeriod="PT1M">
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU utilization" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Privileged Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU privileged time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% User Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU user time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor Information(_Total)\Processor Frequency" sampleRate="PT15S" unit="Count">
            <annotation displayName="CPU frequency" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\System\Processes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Processes" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Thread Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Threads" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Handle Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Handles" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\% Committed Bytes In Use" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Memory usage" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory available" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory committed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Commit Limit" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory commit limit" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Paged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Nonpaged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory non-paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Read Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active read time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Write Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active write time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Transfers/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Reads/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk read operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Writes/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk write operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Read Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk read speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Write Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk write speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Read Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average read queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Write Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average write queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\% Free Space" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk free space (percentage)" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\Free Megabytes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk free space (MB)" locale="en-us"/>
          </PerformanceCounterConfiguration>
        </PerformanceCounters>
        <Metrics resourceId="(Update with resource ID for the VM)" >
            <MetricAggregation scheduledTransferPeriod="PT1H"/>
            <MetricAggregation scheduledTransferPeriod="PT1M"/>
        </Metrics>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*[System[(Level = 1 or Level = 2)]]"/>
          <DataSource name="Security!*[System[(Level = 1 or Level = 2)]"/>
          <DataSource name="System!*[System[(Level = 1 or Level = 2)]]"/>
        </WindowsEventLog>
          </DiagnosticMonitorConfiguration>
        </WadCfg>
        <StorageAccount>(Update with diagnostics storage account name)</StorageAccount>
    </PublicConfig>
    ```

## <a name="next-steps"></a><span data-ttu-id="5d9f1-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5d9f1-141">Next steps</span></span>
* <span data-ttu-id="5d9f1-142">문제 해결을 위한 Azure 진단 기능 및 기타 기법 사용에 대한 추가 지침은 [Azure 클라우드 서비스 및 가상 컴퓨터에서 진단 사용](../../cloud-services/cloud-services-dotnet-diagnostics.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-142">For additional guidance on using the Azure Diagnostics capability and other techniques to troubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="5d9f1-143">[진단 구성 스키마](https://msdn.microsoft.com/library/azure/mt634524.aspx) 는 진단 확장에 대한 다양한 XML 구성 옵션을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9f1-143">[Diagnostics configurations schema](https://msdn.microsoft.com/library/azure/mt634524.aspx) explains the various XML configurations options for the diagnostics extension.</span></span>

