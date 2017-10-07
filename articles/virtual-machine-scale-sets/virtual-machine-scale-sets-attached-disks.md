---
title: "가상 컴퓨터 크기 조정 설정 연결 된 데이터 디스크가 aaaAzure | Microsoft Docs"
description: "Toouse 가상 컴퓨터 크기 집합으로 데이터 디스크를 연결 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: 77b66f80934c0aaf7bb1ad0de00a738052a878ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-attached-data-disks"></a><span data-ttu-id="db9a4-103">Azure VM Scale Sets 및 연결된 데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="db9a4-103">Azure VM scale sets and attached data disks</span></span>
<span data-ttu-id="db9a4-104">이제 Azure [Virtual Machine Scale Sets](/azure/virtual-machine-scale-sets/)은 연결된 데이터 디스크가 있는 가상 컴퓨터를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) now support virtual machines with attached data disks.</span></span> <span data-ttu-id="db9a4-105">데이터 디스크는 Azure 관리 되는 디스크를 사용 하 여 생성 된 크기 집합에 대 한 hello 저장소 프로필에 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-105">Data disks can be defined in hello storage profile for scale sets that have been created with Azure Managed Disks.</span></span> <span data-ttu-id="db9a4-106">이전에 hello에 크기 집합 vm이 사용할 수 있는 유일한 직접 연결 된 저장소 옵션 된 hello 운영 체제 드라이브 및 임시 드라이브입니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-106">Previously hello only directly attached storage options available with VMs in scale sets were hello OS drive and temp drives.</span></span>

> [!NOTE]
>  <span data-ttu-id="db9a4-107">크기 집합으로 정의 된 연결 된 데이터 디스크를 만들 때 toomount 여전히 필요 하면 및 형식 hello 디스크에서 VM toouse 내 (독립 실행형 Azure Vm에 대 한 마찬가지로)을 합니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-107">When you create a scale set with attached data disks defined, you still need toomount and format hello disks from within a VM toouse them (just like for standalone Azure VMs).</span></span> <span data-ttu-id="db9a4-108">편리한 방법을 toodo toouse 표준 스크립트 toopartition를 호출 하 고 VM에서 모든 hello 데이터 디스크를 포맷 하는 사용자 지정 스크립트 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-108">A convenient way toodo this is toouse a custom script extension which calls a standard script toopartition and format all hello data disks on a VM.</span></span>

## <a name="create-a-scale-set-with-attached-data-disks"></a><span data-ttu-id="db9a4-109">연결된 데이터 디스크를 포함한 크기 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="db9a4-109">Create a scale set with attached data disks</span></span>
<span data-ttu-id="db9a4-110">소수 연결 된 디스크를 사용 하 여 설정 하는 간단한 방법을 toocreate는 toouse hello [Azure CLI](https://github.com/Azure/azure-cli) _vmss 만들_ 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-110">A simple way toocreate a scale set with attached disks is toouse hello [Azure CLI](https://github.com/Azure/azure-cli) _vmss create_ command.</span></span> <span data-ttu-id="db9a4-111">다음 예제는 hello는 Azure 리소스 그룹 및 50GB 및 100GB의 2 연결 된 데이터 디스크가 있는 10 개의 Ubuntu Vm의 VM 크기 집합 각각 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-111">hello following example creates an Azure resource group, and a VM scale set of 10 Ubuntu VMs, each with 2 attached data disks, of 50 GB and 100 GB respectively.</span></span>
```bash
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```
<span data-ttu-id="db9a4-112">해당 hello 참고 _vmss 만들_ 명령을 지정 하지 않을 경우 특정 구성 값을 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-112">Note that hello _vmss create_ command defaults certain configuration values if you do not specify them.</span></span> <span data-ttu-id="db9a4-113">시도 재정의할 수 있도록 hello 사용할 수 있는 옵션을 toosee:</span><span class="sxs-lookup"><span data-stu-id="db9a4-113">toosee hello available options that you can override try:</span></span>
```bash
az vmss create --help
```
<span data-ttu-id="db9a4-114">연결 된 데이터 디스크를 사용 하 여 설정 하는 소수 자릿수가 toodefine 눈금에는 Azure 리소스 관리자 템플릿을 설정 하는 또 다른 방법은 toocreate 포함 한 _dataDisks_ hello 섹션인 _storageProfile_, hello를 배포 하 고 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-114">Another way toocreate a scale set with attached data disks is toodefine a scale set in an Azure Resource Manager template, include a _dataDisks_ section in hello _storageProfile_, and deploy hello template.</span></span> <span data-ttu-id="db9a4-115">hello 50GB 및 100GB 디스크 위의 예제 다음과 같이 hello 서식 파일에 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-115">hello 50 GB and 100 GB disk example above would be defined like this in hello template:</span></span>
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
<span data-ttu-id="db9a4-116">여기에 정의 된 연결된 된 디스크와 눈금 집합 서식 파일의 완전 하 고 준비 toodeploy 예제를 확인할 수 있습니다: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data)합니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-116">You can see a complete, ready toodeploy example of a scale set template with an attached disk defined here: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).</span></span>

## <a name="adding-a-data-disk-tooan-existing-scale-set"></a><span data-ttu-id="db9a4-117">데이터 디스크 tooan 기존 확장이 추가 설정</span><span class="sxs-lookup"><span data-stu-id="db9a4-117">Adding a data disk tooan existing scale set</span></span>
> [!NOTE]
>  <span data-ttu-id="db9a4-118">데이터 디스크 tooa 크기 집합으로 작성 된만 연결할 수 있습니다 [Azure 관리 되는 디스크](./virtual-machine-scale-sets-managed-disks.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-118">You can only attach data disks tooa scale set which has been created with [Azure Managed Disks](./virtual-machine-scale-sets-managed-disks.md).</span></span>

<span data-ttu-id="db9a4-119">데이터 디스크 tooa VM 크기 집합 Azure CLI를 사용 하 여 추가할 수 있습니다 _az vmss 디스크 연결_ 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-119">You can add a data disk tooa VM scale set using Azure CLI _az vmss disk attach_ command.</span></span> <span data-ttu-id="db9a4-120">사용될 준비가 되지 않은 lun을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-120">Make sure you specify a lun which is not already in use.</span></span> <span data-ttu-id="db9a4-121">다음 예에서는 CLI hello 50GB 드라이브 toolun을 3을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-121">hello following CLI example adds a 50 GB drive toolun 3:</span></span>
```bash
az vmss disk attach -g dsktest -n dskvmss --size-gb 50 --lun 3
```

<span data-ttu-id="db9a4-122">다음 PowerShell 예에서는 hello 50GB 드라이브 toolun을 3을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-122">hello following PowerShell example adds a 50 GB drive toolun 3:</span></span>
```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName myvmssrg -VMScaleSetName myvmss
$vmss = Add-AzureRmVmssDataDisk -VirtualMachineScaleSet $vmss -Lun 3 -Caching 'ReadWrite' -CreateOption Empty -DiskSizeGB 50 -StorageAccountType StandardLRS
Update-AzureRmVmss -ResourceGroupName myvmssrg -Name myvmss -VirtualMachineScaleSet $vmss
```

> [!NOTE]
> <span data-ttu-id="db9a4-123">다른 VM 크기는 hello 수가 지원 되는 연결 된 드라이브에 서로 다른 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-123">Different VM sizes have different limits on hello numbers of attached drives they support.</span></span> <span data-ttu-id="db9a4-124">Hello 확인 [가상 컴퓨터 크기 특성](../virtual-machines/windows/sizes.md) 새 디스크를 추가 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="db9a4-124">Check hello [virtual machine size characteristics](../virtual-machines/windows/sizes.md) before adding a new disk.</span></span>

<span data-ttu-id="db9a4-125">새 항목 toohello를 추가 하 여 디스크를 추가할 수도 있습니다 _dataDisks_ hello에 대 한 속성 _storageProfile_ 규모의 설정 정의와 hello 변경 내용을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-125">You can also add a disk by adding a new entry toohello _dataDisks_ property in hello _storageProfile_ of a scale set definition and applying hello change.</span></span> <span data-ttu-id="db9a4-126">tootest이,이 찾기 hello 기존 눈금 집합 정의 [Azure 리소스 탐색기](https://resources.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-126">tootest this, find an existing scale set definition in hello [Azure Resource Explorer](https://resources.azure.com/).</span></span> <span data-ttu-id="db9a4-127">선택 _편집_ 데이터 디스크의 새 디스크 toohello 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-127">Select _Edit_ and add a new disk toohello list of data disks.</span></span> <span data-ttu-id="db9a4-128">예:</span><span class="sxs-lookup"><span data-stu-id="db9a4-128">E.g.</span></span> <span data-ttu-id="db9a4-129">위의 hello 예제를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="db9a4-129">using hello example above:</span></span>
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

<span data-ttu-id="db9a4-130">그런 다음 선택 _배치_ tooapply hello tooyour 크기 집합을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-130">Then select _PUT_ tooapply hello changes tooyour scale set.</span></span> <span data-ttu-id="db9a4-131">두 개 이상의 연결된 데이터 디스크를 지원하는 VM 크기를 사용하는 경우 이 예제가 정상적으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-131">This example would work as long as you are using a VM size which supports more than two attached data disks.</span></span>

> [!NOTE]
> <span data-ttu-id="db9a4-132">할 때 변경 tooa 크기 조정 설정 추가 또는 데이터 디스크 제거 같은 정의 tooall 새로 만든 Vm에 적용 됩니다. 하지만 경우에 적용 tooexisting Vm hello _upgradePolicy_ 속성이 "자동" 너무 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-132">When you make a change tooa scale set definition such as adding or removing a data disk, it applies tooall newly created VMs, but only applies tooexisting VMs if hello _upgradePolicy_ property is set too"Automatic".</span></span> <span data-ttu-id="db9a4-133">Toomanually 너무 "수동"으로 설정 하는 경우 해야 hello 새 모델 tooexisting Vm을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-133">If it is set too"Manual", you need toomanually apply hello new model tooexisting VMs.</span></span> <span data-ttu-id="db9a4-134">이렇게 하려면 hello 포털에서 hello를 사용 하 여 _업데이트 AzureRmVmssInstance_ PowerShell 명령 또는 hello를 사용 하 여 _az vmss 업데이트-인스턴스_ CLI 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-134">You can do this in hello portal, using hello _Update-AzureRmVmssInstance_ PowerShell command, or using hello _az vmss update-instances_ CLI command.</span></span>

## <a name="adding-pre-populated-data-disks-tooan-existent-scale-set"></a><span data-ttu-id="db9a4-135">집합을 미리 채워진된 데이터 디스크 tooan 존재 확장이 추가</span><span class="sxs-lookup"><span data-stu-id="db9a4-135">Adding pre-populated data disks tooan existent scale set</span></span> 
> <span data-ttu-id="db9a4-136">기존 디스크 tooan를 추가할 때 스케일 모델을 디자인 하 여, hello 디스크 항상 만들어집니다 빈 합니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-136">When you add disks tooan existent scale set model, by design, hello disk will always be created empty.</span></span> <span data-ttu-id="db9a4-137">이 시나리오는 또한 hello 크기 집합에서 만든 새 인스턴스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-137">This scenario also includes new instances created by hello scale set.</span></span> <span data-ttu-id="db9a4-138">이 동작은 hello scaleset 정의 빈 데이터 디스크 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-138">This behaviour is because hello scaleset definition has an empty data disk.</span></span> <span data-ttu-id="db9a4-139">기존 눈금 집합 모델에 대 한 순서 toocreate 미리 채워진된 데이터 드라이브에서 다음 두 가지 옵션 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-139">In order toocreate pre-populated data drives for an existent scale set model, you can choose either of next two options:</span></span>

* <span data-ttu-id="db9a4-140">데이터 복사 hello 인스턴스 0 VM toohello 데이터 디스크에서 hello에 다른 Vm 사용자 지정 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-140">Copy data from hello instance 0 VM toohello data disk(s) in hello other VMs by running a custom script.</span></span>
* <span data-ttu-id="db9a4-141">Hello OS 디스크 및 (필요한 hello 데이터로) 데이터 디스크와 관리 되는 이미지를 만들고 hello 이미지와 함께 새 scaleset를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-141">Create a managed image with hello OS disk plus data disk (with hello required data) and create a new scaleset with hello image.</span></span> <span data-ttu-id="db9a4-142">이러한 방식으로 만든 모든 새 VM 데이터 갖습니다 디스크 hello scaleset의 hello 정의에 제공 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-142">This way every new VM created will have a data disk that that is provided in hello definition of hello scaleset.</span></span> <span data-ttu-id="db9a4-143">이 정의 사용자 지정 된 데이터에 있는 데이터 디스크를 사용 하 여 tooan 이미지 참조를 이후 hello scaleset에서 모든 가상 컴퓨터 자동으로 나올지 이러한 변경 내용으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-143">Since this definition will refer tooan image with a data disk that has customized data, every virtual machine on hello scaleset will automatically come up with these changes.</span></span>

> <span data-ttu-id="db9a4-144">사용자 지정 이미지를 볼 수 있습니다 하는 방식으로 toocreate hello: [일반화 된 VM의 관리 되는 이미지를 Azure에서 만들기](/azure/virtual-machines/windows/capture-image-resource/)</span><span class="sxs-lookup"><span data-stu-id="db9a4-144">hello way toocreate a custom image can be found here: [Create a managed image of a generalized VM in Azure](/azure/virtual-machines/windows/capture-image-resource/)</span></span> 

> <span data-ttu-id="db9a4-145">hello 사용자에 게 필요한 toocapture hello 필요한 데이터를 hello에 있는 0 VM 인스턴스 선택한 다음 해당 vhd를 사용 하 여 hello 이미지 정의 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-145">hello user needs toocapture hello instance 0 VM which has hello required data, and then use that vhd for hello image definition.</span></span>

## <a name="removing-a-data-disk-from-a-scale-set"></a><span data-ttu-id="db9a4-146">크기 집합에서 데이터 디스크 제거</span><span class="sxs-lookup"><span data-stu-id="db9a4-146">Removing a data disk from a scale set</span></span>
<span data-ttu-id="db9a4-147">Azure CLI _az vmss disk detach_ 명령을 사용하여 VM 크기 집합에서 데이터 디스크를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-147">You can remove a data disk from a VM scale set using Azure CLI _az vmss disk detach_ command.</span></span> <span data-ttu-id="db9a4-148">예를 들어 hello 다음 명령을 제거 lun 2에 정의 된 hello 디스크:</span><span class="sxs-lookup"><span data-stu-id="db9a4-148">For example hello following command removes hello disk defined at lun 2:</span></span>
```bash
az vmss disk detach -g dsktest -n dskvmss --lun 2
```  
<span data-ttu-id="db9a4-149">마찬가지로 제거할 수도 있습니다는 디스크 크기 hello에서 항목을 제거 하 여 집합에서 _dataDisks_ hello에 대 한 속성 _storageProfile_ hello 변경 내용을 적용 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-149">Similarly you can also remove a disk from a scale set by removing an entry from hello _dataDisks_ property in hello _storageProfile_ and applying hello change.</span></span> 

## <a name="additional-notes"></a><span data-ttu-id="db9a4-150">추가적인 참고 사항</span><span class="sxs-lookup"><span data-stu-id="db9a4-150">Additional notes</span></span>
<span data-ttu-id="db9a4-151">Azure 관리 하는 디스크와 소수 연결 된 데이터 디스크 집합에 대 한 지원은 API 버전에서 사용할 수 있는 [ _2016-04-30-미리 보기_ ](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) hello Microsoft.Compute API의 이상.</span><span class="sxs-lookup"><span data-stu-id="db9a4-151">Support for Azure Managed disks and scale set attached data disks is available in API version [_2016-04-30-preview_](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) or later of hello Microsoft.Compute API.</span></span>

<span data-ttu-id="db9a4-152">크기 집합에 대 한 연결 된 디스크 지원의 초기 구현 hello에서에서 연결 하거나 으로/에서 개별 Vm 크기 집합의 데이터 디스크를 분리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-152">In hello initial implementation of attached disk support for scale sets, you cannot attach or detach data disks to/from individual VMs in a scale set.</span></span>

<span data-ttu-id="db9a4-153">크기 집합에 있는 연결된 데이터 디스크에 대한 Azure Portal 지원은 처음부터 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-153">Azure portal support for attached data disks in scale sets is initially limited.</span></span> <span data-ttu-id="db9a4-154">CLI, PowerShell, Sdk 및 REST API toomanage Azure 템플릿을 사용할 수 있습니다 프로그램 요구 사항에 따라 디스크를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="db9a4-154">Depending on your requirements you can use Azure templates, CLI, PowerShell, SDKs, and REST API toomanage attached disks.</span></span>


