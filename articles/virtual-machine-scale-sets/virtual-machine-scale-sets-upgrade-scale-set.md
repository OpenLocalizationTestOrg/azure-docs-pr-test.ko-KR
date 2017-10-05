---
title: "Azure 가상 컴퓨터 확장 집합 업그레이드 | Microsoft Docs"
description: "Azure 가상 컴퓨터 확장 집합 업그레이드"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e229664e-ee4e-4f12-9d2e-a4f456989e5d
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: guybo
ms.openlocfilehash: c7093e221ff8fe69ded1cfbce4f3ddeb1a195666
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a><span data-ttu-id="2fb35-103">가상 컴퓨터 확장 집합 업그레이드</span><span class="sxs-lookup"><span data-stu-id="2fb35-103">Upgrade a virtual machine scale set</span></span>
<span data-ttu-id="2fb35-104">이 문서에서는 가동 중단 시간 없이 OS 업데이트를 Azure 가상 컴퓨터 크기 집합에 롤아웃하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-104">This article describes how you can roll out an OS update to an Azure virtual machine scale set without any downtime.</span></span> <span data-ttu-id="2fb35-105">이 컨텍스트에서 OS 업데이트는 OS의 버전 또는 SKU를 변경하거나 사용자 지정 이미지의 URI를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-105">In this context, an OS update involves changing the version or SKU of the OS or changing the URI of a custom image.</span></span> <span data-ttu-id="2fb35-106">가동 중지 시간 없이 업데이트한다는 것은 가상 컴퓨터를 모두 한꺼번에 업데이트하지 않고 한 번에 하나씩 또는 그룹으로(예" 한 번에 하나의 장애 도메인) 업데이트하는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-106">Updating without downtime means updating virtual machines one at a time or in groups (such as one fault domain at a time) rather than all at once.</span></span> <span data-ttu-id="2fb35-107">이렇게 하면 업그레이드되지 않는 모든 가상 컴퓨터를 계속 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-107">By doing so, any virtual machines that are not being upgraded can keep running.</span></span>

<span data-ttu-id="2fb35-108">모호성을 피하기 위해 수행하려는 네 가지 유형의 OS 업데이트 작업을 구분해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-108">To avoid ambiguity, let’s distinguish four types of OS update you might want to perform:</span></span>

* <span data-ttu-id="2fb35-109">플랫폼 이미지의 버전 또는 SKU 변경.</span><span class="sxs-lookup"><span data-stu-id="2fb35-109">Changing the version or SKU of a platform image.</span></span> <span data-ttu-id="2fb35-110">예를 들어 Ubuntu 14.04.2-LTS 버전을 14.04.201506100에서 14.04.201507060으로 변경하거나 Ubuntu 15.10/최신 SKU를 16.04.0-LTS/최신으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-110">For example, changing Ubuntu 14.04.2-LTS version from 14.04.201506100 to 14.04.201507060, or changing the Ubuntu 15.10/latest SKU to 16.04.0-LTS/latest.</span></span> <span data-ttu-id="2fb35-111">이 시나리오는 이 문서에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-111">This scenario is covered in this article.</span></span>
* <span data-ttu-id="2fb35-112">작성한 새 버전의 사용자 지정 이미지를 가리키는 URI 변경(**속성** > **virtualMachineProfile** > **storageProfile** > **osDisk** > **image** > **uri**).</span><span class="sxs-lookup"><span data-stu-id="2fb35-112">Changing the URI that points to a new version of a custom image you built (**properties** > **virtualMachineProfile** > **storageProfile** > **osDisk** > **image** > **uri**).</span></span> <span data-ttu-id="2fb35-113">이 시나리오는 이 문서에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-113">This scenario is covered in this article.</span></span>
* <span data-ttu-id="2fb35-114">Azure Managed Disks를 사용하여 만든 확장 집합의 이미지 참조 변경.</span><span class="sxs-lookup"><span data-stu-id="2fb35-114">Changing the image reference of a scale set that was created using Azure Managed Disks.</span></span>
* <span data-ttu-id="2fb35-115">가상 컴퓨터 내에서 OS 패치(이 예제에는 보안 패치 설치 및 Windows 업데이트 실행 포함).</span><span class="sxs-lookup"><span data-stu-id="2fb35-115">Patching the OS from within a virtual machine (examples of this include installing a security patch and running Windows Update).</span></span> <span data-ttu-id="2fb35-116">이 시나리오는 지원되지만 이 문서에서는 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-116">This scenario is supported but not covered in this article.</span></span>

<span data-ttu-id="2fb35-117">[Azure 서비스 패브릭](https://azure.microsoft.com/services/service-fabric/) 클러스터의 일부로 배포되는 가상 컴퓨터 크기 집합은 여기에서 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-117">Virtual machine scale sets that are deployed as part of an [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) cluster are not covered here.</span></span> <span data-ttu-id="2fb35-118">서비스 패브릭 패치에 대한 자세한 내용은 [Service Fabric 클러스터에서 Windows OS 패치](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb35-118">See [Patch Windows OS in your Service Fabric cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) for more information about patching Service Fabric.</span></span>

<span data-ttu-id="2fb35-119">플랫폼 이미지의 OS 버전/SKU나 사용자 지정 이미지의 URI를 변경하기 위한 기본 순서는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-119">The basic sequence for changing the OS version/SKU of a platform image or the URI of a custom image looks as follows:</span></span>

1. <span data-ttu-id="2fb35-120">가상 컴퓨터 크기 집합 모델을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-120">Get the virtual machine scale set model.</span></span>
2. <span data-ttu-id="2fb35-121">모델에서 버전, SKU, 이미지 참조 또는 URI 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-121">Change the version, SKU, image reference, or URI value in the model.</span></span>
3. <span data-ttu-id="2fb35-122">모델을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-122">Update the model.</span></span>
4. <span data-ttu-id="2fb35-123">크기 집합의 가상 컴퓨터에 대해 *manualUpgrade* 호출을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-123">Do a *manualUpgrade* call on the virtual machines in the scale set.</span></span> <span data-ttu-id="2fb35-124">이 단계는 크기 집합의 *upgradePolicy* 속성이 **수동** 으로 설정된 경우만 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-124">This step is only relevant if *upgradePolicy* is set to **Manual** in your scale set.</span></span> <span data-ttu-id="2fb35-125">**자동**으로 설정되면 모든 가상 컴퓨터가 한꺼번에 업그레이드되므로 가동 중지 시간이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-125">If it is set to **Automatic**, all the virtual machines are upgraded at once, thus causing downtime.</span></span>

<span data-ttu-id="2fb35-126">이 정보를 염두에 두고 PowerShell에서 또는 REST API를 사용하여 확장 집합의 버전을 업데이트하는 방법을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-126">With this information in mind, let’s see how you could update the version of a scale set in PowerShell, and by using the REST API.</span></span> <span data-ttu-id="2fb35-127">이러한 예제는 플랫폼 이미지의 경우를 포함하지만, 이 문서에서는 이 프로세스를 사용자 지정 이미지에 맞게 조정하기 위한 충분한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-127">These examples cover the case of a platform image, but this article provides enough information for you to adapt this process to a custom image.</span></span>

## <a name="powershell"></a><span data-ttu-id="2fb35-128">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fb35-128">PowerShell</span></span>
<span data-ttu-id="2fb35-129">이 예제에서는 Windows 가상 컴퓨터 확장 집합을 새 버전인 4.0.20160229로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-129">This example updates a Windows virtual machine scale set (creating to the new version 4.0.20160229.</span></span> <span data-ttu-id="2fb35-130">모델을 업데이트한 후 한 번에 하나의 가상 컴퓨터 인스턴스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-130">After updating the model, it does an update one virtual machine instance at a time.</span></span>

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get the VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set the new version in the model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update the virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

<span data-ttu-id="2fb35-131">플랫폼 이미지 버전을 변경하는 대신 사용자 지정 이미지의 URI를 업데이트하는 경우 “새 버전 설정” 줄을 원본 이미지 URI을 업데이트하는 명령으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-131">If you are updating the URI for a custom image instead of changing a platform image version, replace the “set the new version” line with a command that will update the source image URI.</span></span> <span data-ttu-id="2fb35-132">예를 들어 Azure Managed Disks를 사용하지 않고 확장 집합을 만든 경우 업데이트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-132">For example, if the scale set was created without using Azure Managed Disks, the update would look like this:</span></span>

```powershell
# set the new version in the model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

<span data-ttu-id="2fb35-133">Azure Managed Disks를 사용하여 사용자 지정 이미지 기반 확장 집합을 만든 경우 이미지 참조가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-133">If a custom image based scale set was created using Azure Managed Disks, then the image reference would be updated.</span></span> <span data-ttu-id="2fb35-134">예:</span><span class="sxs-lookup"><span data-stu-id="2fb35-134">For example:</span></span>

```powershell
# set the new version in the model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="the-rest-api"></a><span data-ttu-id="2fb35-135">REST API</span><span class="sxs-lookup"><span data-stu-id="2fb35-135">The REST API</span></span>
<span data-ttu-id="2fb35-136">다음은 Azure REST API를 사용하여 OS 버전 업데이트를 롤아웃하는 Python의 몇 가지 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-136">Here are a couple of Python examples that use the Azure REST API to roll out an OS version update.</span></span> <span data-ttu-id="2fb35-137">두 가지 모두 Azure REST API 래퍼 함수의 경량 [azurerm](https://pypi.python.org/pypi/azurerm) 라이브러리를 사용하여 크기 집합 모델에 대해 GET을 수행한 다음 업데이트된 모델에 대해 PUT을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-137">Both use the lightweight [azurerm](https://pypi.python.org/pypi/azurerm) library of Azure REST API wrapper functions to do a GET on the scale set model, followed by a PUT with an updated model.</span></span> <span data-ttu-id="2fb35-138">또한 업데이트 도메인으로 가상 컴퓨터를 식별하기 위해 가상 컴퓨터 인스턴스 보기도 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-138">They also look at virtual machine instances views to identify the virtual machines by update domain.</span></span>

### <a name="vmssupgrade"></a><span data-ttu-id="2fb35-139">Vmssupgrade</span><span class="sxs-lookup"><span data-stu-id="2fb35-139">Vmssupgrade</span></span>
 <span data-ttu-id="2fb35-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) 는 한 번에 한 업데이트 도메인씩, 실행 중인 가상 컴퓨터 크기 집합으로 OS 업그레이드를 롤아웃하는 데 사용되는 Python 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) is a Python script that's used to roll out an OS upgrade to a running virtual machine scale set one update domain at a time.</span></span>

![가상 컴퓨터 또는 업데이트 도메인을 선택하기 위한 Vmssupgrade 스크립트](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

<span data-ttu-id="2fb35-142">이 스크립트를 통해 특정 가상 컴퓨터를 선택하여 업데이트 도메인을 업데이트하거나 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-142">This script lets you choose specific virtual machines to update or specify an update domain.</span></span> <span data-ttu-id="2fb35-143">이 스크립트는 플랫폼 이미지 버전 변경 또는 사용자 지정 이미지의 URI 변경을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-143">It supports changing a platform image version or changing the URI of a custom image.</span></span>

### <a name="vmsseditor"></a><span data-ttu-id="2fb35-144">Vmsseditor</span><span class="sxs-lookup"><span data-stu-id="2fb35-144">Vmsseditor</span></span>
<span data-ttu-id="2fb35-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) 는 한 행이 하나의 업데이트 도메인을 나타내는 heatmap으로 가상 컴퓨터 상태를 표시하는 가상 컴퓨터 크기 집합에 대한 범용 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) is a general-purpose editor for virtual machine scale sets that shows virtual machine status as a heatmap where one row represents one update domain.</span></span> <span data-ttu-id="2fb35-146">무엇보다도 새 버전의 SKU 또는 사용자 지정 이미지 URI로 크기 집합에 대한 모델을 업데이트한 다음 업그레이드할 장애 도메인을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-146">Among other things, you can update the model for a scale set with a new version, SKU, or custom image URI, and then pick fault domains to upgrade.</span></span> <span data-ttu-id="2fb35-147">이렇게 하면 해당 업데이트 도메인에 있는 모든 가상 컴퓨터가 새 모델로 업그레이드됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-147">When you do so, all the virtual machines in that update domain are upgraded to the new model.</span></span> <span data-ttu-id="2fb35-148">또는 선택한 배치 크기에 따라 롤링 업그레이드를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-148">Alternatively, you can do a rolling upgrade based on the batch size of your choice.</span></span>  

<span data-ttu-id="2fb35-149">다음 스크린샷에서는 Ubuntu 14.04 2LTS 버전 14.04.201507060에 대한 크기 집합 모델을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-149">The following screenshot shows a model of a scale set for Ubuntu 14.04-2LTS version 14.04.201507060.</span></span> <span data-ttu-id="2fb35-150">이 스크린샷이 작성된 이후에 추가 옵션이 이 도구에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-150">Many more options have been added to this tool since this screenshot was taken.</span></span>

![Ubuntu 14.04-2LTS에 대한 크기 집합의 Vmsseditor 모델](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

<span data-ttu-id="2fb35-152">**업그레이드**를 클릭한 후 **세부 정보 보기**를 클릭하면 UD 0의 가상 컴퓨터가 업데이트되기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb35-152">After you click **Upgrade** and then **Get Details**, virtual machines in UD 0 start to update.</span></span>

![진행 중인 업데이트를 보여 주는 Vmsseditor](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)

