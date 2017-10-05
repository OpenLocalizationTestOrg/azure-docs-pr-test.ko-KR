---
title: "Azure Virtual Machine Scale Sets 연결 데이터 디스크 | Microsoft Docs"
description: "가상 컴퓨터 크기 집합과 연결된 데이터 디스크를 사용하는 방법 알아보기"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/25/2017
ms.author: guybo
ms.openlocfilehash: 22c7e589efa9a9f401549ec9b95c58c4eaf07b94
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-vm-scale-sets-and-attached-data-disks"></a><span data-ttu-id="5b770-103">Azure VM Scale Sets 및 연결된 데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="5b770-103">Azure VM scale sets and attached data disks</span></span>
<span data-ttu-id="5b770-104">이제 Azure [Virtual Machine Scale Sets](/azure/virtual-machine-scale-sets/)은 연결된 데이터 디스크가 있는 가상 컴퓨터를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) now support virtual machines with attached data disks.</span></span> <span data-ttu-id="5b770-105">Azure Managed Disks를 사용하여 만든 확장 집합에 대한 저장소 프로필에서 데이터 디스크를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-105">Data disks can be defined in the storage profile for scale sets that have been created with Azure Managed Disks.</span></span> <span data-ttu-id="5b770-106">이전에 크기 집합에서 VM과 함께 사용할 수 있는 직접 연결된 저장소 옵션에는 OS 드라이브 및 임시 드라이브가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-106">Previously the only directly attached storage options available with VMs in scale sets were the OS drive and temp drives.</span></span>

> [!NOTE]
>  <span data-ttu-id="5b770-107">정의된 연결된 데이터 디스크를 사용하여 크기 집합을 만드는 경우 독립 실행형 Azure VM의 경우와 마찬가지로 사용할 VM 내에서 디스크를 탑재하고 포맷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-107">When you create a scale set with attached data disks defined, you still need to mount and format the disks from within a VM to use them (just like for standalone Azure VMs).</span></span> <span data-ttu-id="5b770-108">이 작업을 수행하는 편리한 방법은 사용자 지정 스크립트 확장을 사용하여 VM에서 모든 데이터 디스크를 분할하고 포맷하는 표준 스크립트를 호출하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-108">A convenient way to do this is to use a custom script extension which calls a standard script to partition and format all the data disks on a VM.</span></span>

## <a name="create-a-scale-set-with-attached-data-disks"></a><span data-ttu-id="5b770-109">연결된 데이터 디스크를 포함한 크기 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="5b770-109">Create a scale set with attached data disks</span></span>
<span data-ttu-id="5b770-110">연결된 디스크를 포함하는 크기 집합을 만드는 간단한 방법은 [Azure CLI](https://github.com/Azure/azure-cli) _vmss create_ 명령을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-110">A simple way to create a scale set with attached disks is to use the [Azure CLI](https://github.com/Azure/azure-cli) _vmss create_ command.</span></span> <span data-ttu-id="5b770-111">다음 예제에서는 Azure 리소스 그룹 및 각각 50GB 및 100GB라는 두 개의 연결된 데이터 디스크를 포함한 10개의 Ubuntu VM인 VM 크기 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-111">The following example creates an Azure resource group, and a VM scale set of 10 Ubuntu VMs, each with 2 attached data disks, of 50 GB and 100 GB respectively.</span></span>
```bash
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```
<span data-ttu-id="5b770-112">_vmss create_ 명령을 지정하지 않으면 특정 구성 값을 기본값으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-112">Note that the _vmss create_ command defaults certain configuration values if you do not specify them.</span></span> <span data-ttu-id="5b770-113">재정의할 수 있는 사용 가능한 옵션을 확인하려면 다음을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="5b770-113">To see the available options that you can override try:</span></span>
```bash
az vmss create --help
```
<span data-ttu-id="5b770-114">연결된 데이터 디스크를 포함한 크기 집합을 만드는 또 다른 방법은 Azure Resource Manager 템플릿에서 크기 집합을 정의하고 _storageProfile_에서 _dataDisks_ 섹션을 포함하며 템플릿을 배포하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-114">Another way to create a scale set with attached data disks is to define a scale set in an Azure Resource Manager template, include a _dataDisks_ section in the _storageProfile_, and deploy the template.</span></span> <span data-ttu-id="5b770-115">위에 있는 50GB 및 100GB 디스크 예제는 템플릿에서 다음과 같이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-115">The 50 GB and 100 GB disk example above would be defined like this in the template:</span></span>
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    }
]
```
<span data-ttu-id="5b770-116">다음에 정의된 연결된 디스크를 포함한 크기 집합 템플릿의 예제를 배포하기 위해 완벽하게 준비되었습니다. [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data)</span><span class="sxs-lookup"><span data-stu-id="5b770-116">You can see a complete, ready to deploy example of a scale set template with an attached disk defined here: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).</span></span>

## <a name="adding-a-data-disk-to-an-existing-scale-set"></a><span data-ttu-id="5b770-117">기존 크기 집합에 데이터 디스크 추가</span><span class="sxs-lookup"><span data-stu-id="5b770-117">Adding a data disk to an existing scale set</span></span>
> [!NOTE]
>  <span data-ttu-id="5b770-118">[Azure Managed Disks](./virtual-machine-scale-sets-managed-disks.md)를 사용하여 만든 확장 집합에만 데이터 디스크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-118">You can only attach data disks to a scale set which has been created with [Azure Managed Disks](./virtual-machine-scale-sets-managed-disks.md).</span></span>

<span data-ttu-id="5b770-119">Azure CLI _az vmss disk attach_ 명령을 사용하여 VM 크기 집합에 데이터 디스크를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-119">You can add a data disk to a VM scale set using Azure CLI _az vmss disk attach_ command.</span></span> <span data-ttu-id="5b770-120">사용될 준비가 되지 않은 lun을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-120">Make sure you specify a lun which is not already in use.</span></span> <span data-ttu-id="5b770-121">다음 CLI 예제는 50GB 드라이브를 lun 3에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-121">The following CLI example adds a 50 GB drive to lun 3:</span></span>
```bash
az vmss disk attach -g dsktest -n dskvmss --size-gb 50 --lun 3
```

<span data-ttu-id="5b770-122">다음 PowerShell 예제는 50GB 드라이브를 lun 3에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-122">The following PowerShell example adds a 50 GB drive to lun 3:</span></span>
```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName myvmssrg -VMScaleSetName myvmss
$vmss = Add-AzureRmVmssDataDisk -VirtualMachineScaleSet $vmss -Lun 3 -Caching 'ReadWrite' -CreateOption Empty -DiskSizeGB 50 -StorageAccountType StandardLRS
Update-AzureRmVmss -ResourceGroupName myvmssrg -Name myvmss -VirtualMachineScaleSet $vmss
```

> [!NOTE]
> <span data-ttu-id="5b770-123">다양한 VM 크기에 따라 지원하는 연결된 드라이브의 숫자가 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-123">Different VM sizes have different limits on the numbers of attached drives they support.</span></span> <span data-ttu-id="5b770-124">새 디스크를 추가하기 전에 [가상 컴퓨터 크기 특성](../virtual-machines/windows/sizes.md)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-124">Check the [virtual machine size characteristics](../virtual-machines/windows/sizes.md) before adding a new disk.</span></span>

<span data-ttu-id="5b770-125">크기 집합 정의의 _storageProfile_에 있는 _dataDisks_ 속성에 새 항목을 추가하고 변경 내용을 적용하여 디스크를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-125">You can also add a disk by adding a new entry to the _dataDisks_ property in the _storageProfile_ of a scale set definition and applying the change.</span></span> <span data-ttu-id="5b770-126">이를 테스트하려면 [Azure 리소스 탐색기](https://resources.azure.com/)에서 기존 크기 집합을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-126">To test this, find an existing scale set definition in the [Azure Resource Explorer](https://resources.azure.com/).</span></span> <span data-ttu-id="5b770-127">_편집_을 선택하고 데이터 디스크의 목록에 새 디스크를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-127">Select _Edit_ and add a new disk to the list of data disks.</span></span> <span data-ttu-id="5b770-128">예:</span><span class="sxs-lookup"><span data-stu-id="5b770-128">E.g.</span></span> <span data-ttu-id="5b770-129">위의 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-129">using the example above:</span></span>
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    },
    {
    "lun": 3,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 20
    }          
]
```

<span data-ttu-id="5b770-130">_배치_를 선택하여 크기 집합에 변경 내용을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-130">Then select _PUT_ to apply the changes to your scale set.</span></span> <span data-ttu-id="5b770-131">두 개 이상의 연결된 데이터 디스크를 지원하는 VM 크기를 사용하는 경우 이 예제가 정상적으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-131">This example would work as long as you are using a VM size which supports more than two attached data disks.</span></span>

> [!NOTE]
> <span data-ttu-id="5b770-132">데이터 디스크를 추가하거나 제거하는 등 크기 집합 정의를 변경하는 경우 새로 만든 VM에 적용되지만 _upgradePolicy_ 속성이 "자동"으로 설정된 경우 기존 VM에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-132">When you make a change to a scale set definition such as adding or removing a data disk, it applies to all newly created VMs, but only applies to existing VMs if the _upgradePolicy_ property is set to "Automatic".</span></span> <span data-ttu-id="5b770-133">"수동"으로 설정하면 수동으로 기존 VM에 새 모델을 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-133">If it is set to "Manual", you need to manually apply the new model to existing VMs.</span></span> <span data-ttu-id="5b770-134">포털에서 _Update-AzureRmVmssInstance_ PowerShell 명령 또는 _az vmss update-instances_ CLI 명령을 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-134">You can do this in the portal, using the _Update-AzureRmVmssInstance_ PowerShell command, or using the _az vmss update-instances_ CLI command.</span></span>

## <a name="adding-pre-populated-data-disks-to-an-existent-scale-set"></a><span data-ttu-id="5b770-135">기존 확장 집합에 미리 지정된 데이터 디스크 추가</span><span class="sxs-lookup"><span data-stu-id="5b770-135">Adding pre-populated data disks to an existent scale set</span></span> 
> <span data-ttu-id="5b770-136">확장 집합에 디스크를 추가하는 경우 설계 상 디스크는 항상 비어 있게 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-136">When you add disks to an existent scale set model, by design, the disk will always be created empty.</span></span> <span data-ttu-id="5b770-137">이 시나리오는 확장 집합에서 만든 새 인스턴스도 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-137">This scenario also includes new instances created by the scale set.</span></span> <span data-ttu-id="5b770-138">확장 집합 정의에 빈 데이터 디스크가 있기 때문에 이 동작이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-138">This behaviour is because the scaleset definition has an empty data disk.</span></span> <span data-ttu-id="5b770-139">기존 확장 집합 모델에 미리 지정된 데이터 드라이브를 만들기 위해 다음 두 가지 옵션 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-139">In order to create pre-populated data drives for an existent scale set model, you can choose either of next two options:</span></span>

* <span data-ttu-id="5b770-140">사용자 지정 스크립트를 실행하여 인스턴스 0 VM에서 다른 VM의 데이터 디스크에 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-140">Copy data from the instance 0 VM to the data disk(s) in the other VMs by running a custom script.</span></span>
* <span data-ttu-id="5b770-141">OS 디스크 및 데이터 디스크(필요한 데이터 포함)에서 관리되는 이미지를 만들고 이미지를 포함한 새 확장 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-141">Create a managed image with the OS disk plus data disk (with the required data) and create a new scaleset with the image.</span></span> <span data-ttu-id="5b770-142">이러한 방식으로 만든 모든 새 VM에는 확장 집합의 정의에 제공되는 데이터 디스크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-142">This way every new VM created will have a data disk that that is provided in the definition of the scaleset.</span></span> <span data-ttu-id="5b770-143">이 정의가 사용자 지정된 데이터를 포함한 데이터 디스크를 사용하여 이미지를 참조하기 때문에 확장 집합의 모든 가상 컴퓨터는 이러한 변경 내용을 자동으로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-143">Since this definition will refer to an image with a data disk that has customized data, every virtual machine on the scaleset will automatically come up with these changes.</span></span>

> <span data-ttu-id="5b770-144">사용자 지정 이미지를 만들 수 있는 방법은 [Azure에서 일반화된 VM의 관리되는 이미지 만들기](/azure/virtual-machines/windows/capture-image-resource/)에서 확인할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="5b770-144">The way to create a custom image can be found here: [Create a managed image of a generalized VM in Azure](/azure/virtual-machines/windows/capture-image-resource/)</span></span> 

> <span data-ttu-id="5b770-145">사용자는 필수 데이터를 포함한 인스턴스 0 VM을 캡처해야 하고 이미지 정의에 VHD를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-145">The user needs to capture the instance 0 VM which has the required data, and then use that vhd for the image definition.</span></span>

## <a name="removing-a-data-disk-from-a-scale-set"></a><span data-ttu-id="5b770-146">크기 집합에서 데이터 디스크 제거</span><span class="sxs-lookup"><span data-stu-id="5b770-146">Removing a data disk from a scale set</span></span>
<span data-ttu-id="5b770-147">Azure CLI _az vmss disk detach_ 명령을 사용하여 VM 크기 집합에서 데이터 디스크를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-147">You can remove a data disk from a VM scale set using Azure CLI _az vmss disk detach_ command.</span></span> <span data-ttu-id="5b770-148">예를 들어, 다음 명령은 lun 2에 정의된 디스크를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-148">For example the following command removes the disk defined at lun 2:</span></span>
```bash
az vmss disk detach -g dsktest -n dskvmss --lun 2
```  
<span data-ttu-id="5b770-149">마찬가지로 _storageProfile_에 있는 _dataDisks_ 속성에서 항목을 제거하고 변경 내용을 적용하여 크기 집합에서 디스크를 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-149">Similarly you can also remove a disk from a scale set by removing an entry from the _dataDisks_ property in the _storageProfile_ and applying the change.</span></span> 

## <a name="additional-notes"></a><span data-ttu-id="5b770-150">추가적인 참고 사항</span><span class="sxs-lookup"><span data-stu-id="5b770-150">Additional notes</span></span>
<span data-ttu-id="5b770-151">Azure Managed Disks 및 확장 집합 연결 데이터 디스크에 대한 지원은 Microsoft.Compute API [_2016-04-30-preview_](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) 이상의 API 버전에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-151">Support for Azure Managed disks and scale set attached data disks is available in API version [_2016-04-30-preview_](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) or later of the Microsoft.Compute API.</span></span>

<span data-ttu-id="5b770-152">크기 집합에 대한 연결된 디스크 지원의 초기 구현 중에 크기 집합에 있는 개별 VM 간에 데이터 디스크를 연결하거나 분리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-152">In the initial implementation of attached disk support for scale sets, you cannot attach or detach data disks to/from individual VMs in a scale set.</span></span>

<span data-ttu-id="5b770-153">크기 집합에 있는 연결된 데이터 디스크에 대한 Azure Portal 지원은 처음부터 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-153">Azure portal support for attached data disks in scale sets is initially limited.</span></span> <span data-ttu-id="5b770-154">요구 사항에 따라 Azure 템플릿, CLI, PowerShell, SDK 및 REST API를 사용하여 연결된 디스크를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b770-154">Depending on your requirements you can use Azure templates, CLI, PowerShell, SDKs, and REST API to manage attached disks.</span></span>


