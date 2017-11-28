---
title: "aaaUpgrade Azure 가상 컴퓨터 크기 집합 | Microsoft Docs"
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
ms.openlocfilehash: 068e98503f8d37ea71e45b8673a01da2e814f521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a><span data-ttu-id="62b65-103">가상 컴퓨터 확장 집합 업그레이드</span><span class="sxs-lookup"><span data-stu-id="62b65-103">Upgrade a virtual machine scale set</span></span>
<span data-ttu-id="62b65-104">이 문서는 OS 업데이트 tooan Azure 가상 컴퓨터 크기 집합 가동 중지 시간 없이 롤아웃할 수는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-104">This article describes how you can roll out an OS update tooan Azure virtual machine scale set without any downtime.</span></span> <span data-ttu-id="62b65-105">이 컨텍스트에서에서 OS 업데이트 하려면 hello 사용자 지정 이미지의 URI를 변경 하거나 hello 버전 또는 hello OS의 SKU를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-105">In this context, an OS update involves changing hello version or SKU of hello OS or changing hello URI of a custom image.</span></span> <span data-ttu-id="62b65-106">가동 중지 시간 없이 업데이트한다는 것은 가상 컴퓨터를 모두 한꺼번에 업데이트하지 않고 한 번에 하나씩 또는 그룹으로(예" 한 번에 하나의 장애 도메인) 업데이트하는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-106">Updating without downtime means updating virtual machines one at a time or in groups (such as one fault domain at a time) rather than all at once.</span></span> <span data-ttu-id="62b65-107">이렇게 하면 업그레이드되지 않는 모든 가상 컴퓨터를 계속 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-107">By doing so, any virtual machines that are not being upgraded can keep running.</span></span>

<span data-ttu-id="62b65-108">tooavoid 모호성을 보겠습니다 네 가지 유형의 할 수 있습니다는 OS 업데이트를 구분할 tooperform:</span><span class="sxs-lookup"><span data-stu-id="62b65-108">tooavoid ambiguity, let’s distinguish four types of OS update you might want tooperform:</span></span>

* <span data-ttu-id="62b65-109">Hello 버전 또는 플랫폼 이미지의 SKU를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-109">Changing hello version or SKU of a platform image.</span></span> <span data-ttu-id="62b65-110">예를 들어, Ubuntu 변경 14.04.201506100에서 14.04.2-LTS 버전 too14.04.201507060, 또는 hello Ubuntu 15.10/가장 늦은 SKU too16.04.0-LTS/latest 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-110">For example, changing Ubuntu 14.04.2-LTS version from 14.04.201506100 too14.04.201507060, or changing hello Ubuntu 15.10/latest SKU too16.04.0-LTS/latest.</span></span> <span data-ttu-id="62b65-111">이 시나리오는 이 문서에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-111">This scenario is covered in this article.</span></span>
* <span data-ttu-id="62b65-112">사용자 지정 이미지를 빌드한 tooa 새 버전을 가리키는 URI를 hello 변경 (**속성** > **virtualMachineProfile** > **storageProfile**  >  **osDisk** > **이미지** > **uri**).</span><span class="sxs-lookup"><span data-stu-id="62b65-112">Changing hello URI that points tooa new version of a custom image you built (**properties** > **virtualMachineProfile** > **storageProfile** > **osDisk** > **image** > **uri**).</span></span> <span data-ttu-id="62b65-113">이 시나리오는 이 문서에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-113">This scenario is covered in this article.</span></span>
* <span data-ttu-id="62b65-114">Azure 관리 되는 디스크를 사용 하 여 만든 크기 집합의 hello 이미지 참조를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-114">Changing hello image reference of a scale set that was created using Azure Managed Disks.</span></span>
* <span data-ttu-id="62b65-115">가상 컴퓨터 내에서 OS hello 패치 (이 예에서는 보안 패치를 설치 하 고 Windows 업데이트 실행을 포함 하는 데 사용).</span><span class="sxs-lookup"><span data-stu-id="62b65-115">Patching hello OS from within a virtual machine (examples of this include installing a security patch and running Windows Update).</span></span> <span data-ttu-id="62b65-116">이 시나리오는 지원되지만 이 문서에서는 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-116">This scenario is supported but not covered in this article.</span></span>

<span data-ttu-id="62b65-117">[Azure 서비스 패브릭](https://azure.microsoft.com/services/service-fabric/) 클러스터의 일부로 배포되는 가상 컴퓨터 크기 집합은 여기에서 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-117">Virtual machine scale sets that are deployed as part of an [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) cluster are not covered here.</span></span> <span data-ttu-id="62b65-118">서비스 패브릭 패치에 대한 자세한 내용은 [Service Fabric 클러스터에서 Windows OS 패치](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="62b65-118">See [Patch Windows OS in your Service Fabric cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) for more information about patching Service Fabric.</span></span>

<span data-ttu-id="62b65-119">hello 기본 시퀀스 변경에 대 한 hello OS 버전/플랫폼 이미지의 SKU 또는 사용자 지정 이미지의 URI hello 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-119">hello basic sequence for changing hello OS version/SKU of a platform image or hello URI of a custom image looks as follows:</span></span>

1. <span data-ttu-id="62b65-120">Hello 가상 컴퓨터 크기 조정 설정 모델을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-120">Get hello virtual machine scale set model.</span></span>
2. <span data-ttu-id="62b65-121">Hello 버전, SKU, 이미지 참조 또는 hello 모델에 대 한 URI 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-121">Change hello version, SKU, image reference, or URI value in hello model.</span></span>
3. <span data-ttu-id="62b65-122">Hello 모델을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-122">Update hello model.</span></span>
4. <span data-ttu-id="62b65-123">수행 된 *manualUpgrade* hello 크기 집합의 hello 가상 컴퓨터에서 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-123">Do a *manualUpgrade* call on hello virtual machines in hello scale set.</span></span> <span data-ttu-id="62b65-124">이 단계는 관련만 경우 *upgradePolicy* 너무 설정**수동** 프로그램 규모에 맞게 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-124">This step is only relevant if *upgradePolicy* is set too**Manual** in your scale set.</span></span> <span data-ttu-id="62b65-125">너무 설정 되어 있으면**자동**, 가동 중지 시간 오류를 발생 시킬 모든 hello 가상 컴퓨터를 한 번에 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-125">If it is set too**Automatic**, all hello virtual machines are upgraded at once, thus causing downtime.</span></span>

<span data-ttu-id="62b65-126">이 정보에 주의 hello 버전 및 hello REST API를 사용 하 여 PowerShell에 설정 해 규모의 업데이트 수는 어떻게 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-126">With this information in mind, let’s see how you could update hello version of a scale set in PowerShell, and by using hello REST API.</span></span> <span data-ttu-id="62b65-127">이러한 예제는 플랫폼 이미지의 hello 대/소문자를 포함 하지만이 문서에서는이 프로세스 tooa 사용자 지정 이미지 tooadapt 하기에 충분 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-127">These examples cover hello case of a platform image, but this article provides enough information for you tooadapt this process tooa custom image.</span></span>

## <a name="powershell"></a><span data-ttu-id="62b65-128">PowerShell</span><span class="sxs-lookup"><span data-stu-id="62b65-128">PowerShell</span></span>
<span data-ttu-id="62b65-129">이 예에서는 업데이트는 Windows 가상 컴퓨터 크기 집합 (만드는 toohello 새로운 버전 4.0.20160229입니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-129">This example updates a Windows virtual machine scale set (creating toohello new version 4.0.20160229.</span></span> <span data-ttu-id="62b65-130">Hello 모델을 업데이트 한 다음 한 번에 하나의 가상 컴퓨터 인스턴스는 업데이트 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-130">After updating hello model, it does an update one virtual machine instance at a time.</span></span>

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get hello VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update hello virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

<span data-ttu-id="62b65-131">플랫폼 이미지 버전을 변경 하는 대신 사용자 지정 이미지에 대 한 URI hello를 업데이트 하는 경우 대체 hello "집합 hello 새 버전"를 업데이트 하는 명령 사용 하 여 줄 hello 소스 이미지 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-131">If you are updating hello URI for a custom image instead of changing a platform image version, replace hello “set hello new version” line with a command that will update hello source image URI.</span></span> <span data-ttu-id="62b65-132">예를 들어 hello 크기 집합을 만들어진 경우 Azure 관리 되는 디스크를 사용 하지 않고 hello 업데이트 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-132">For example, if hello scale set was created without using Azure Managed Disks, hello update would look like this:</span></span>

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

<span data-ttu-id="62b65-133">사용자 지정 이미지에 크기 집합 기반를 만든 경우 Azure 관리 되는 디스크를 사용 하 여 후 hello 이미지 참조를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-133">If a custom image based scale set was created using Azure Managed Disks, then hello image reference would be updated.</span></span> <span data-ttu-id="62b65-134">예:</span><span class="sxs-lookup"><span data-stu-id="62b65-134">For example:</span></span>

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="hello-rest-api"></a><span data-ttu-id="62b65-135">hello REST API</span><span class="sxs-lookup"><span data-stu-id="62b65-135">hello REST API</span></span>
<span data-ttu-id="62b65-136">다음은 몇 가지 hello Azure REST API tooroll OS 버전 업데이트를 사용 하는 Python 예입니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-136">Here are a couple of Python examples that use hello Azure REST API tooroll out an OS version update.</span></span> <span data-ttu-id="62b65-137">둘 다 사용 hello lightweight [azurerm](https://pypi.python.org/pypi/azurerm) Azure REST API 래퍼 함수 toodo GET hello 눈금에서의 라이브러리 설정 모델을 업데이트 된 모델 PUT 옵니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-137">Both use hello lightweight [azurerm](https://pypi.python.org/pypi/azurerm) library of Azure REST API wrapper functions toodo a GET on hello scale set model, followed by a PUT with an updated model.</span></span> <span data-ttu-id="62b65-138">또한 살펴봅니다 가상 컴퓨터 인스턴스 뷰 업데이트 도메인이 tooidentify hello 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="62b65-138">They also look at virtual machine instances views tooidentify hello virtual machines by update domain.</span></span>

### <a name="vmssupgrade"></a><span data-ttu-id="62b65-139">Vmssupgrade</span><span class="sxs-lookup"><span data-stu-id="62b65-139">Vmssupgrade</span></span>
 <span data-ttu-id="62b65-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) 은 가상 컴퓨터 크기를 실행 중인 운영 체제 업그레이드 tooa 아웃 tooroll가 사용 하는 Python 스크립트 한 번에 하나의 업데이트 도메인을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) is a Python script that's used tooroll out an OS upgrade tooa running virtual machine scale set one update domain at a time.</span></span>

![가상 컴퓨터 또는 업데이트 도메인을 선택하기 위한 Vmssupgrade 스크립트](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

<span data-ttu-id="62b65-142">이 스크립트를 사용 하면 tooupdate 특정 가상 컴퓨터를 선택 하거나 업데이트 도메인을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-142">This script lets you choose specific virtual machines tooupdate or specify an update domain.</span></span> <span data-ttu-id="62b65-143">Hello 사용자 지정 이미지의 URI를 변경 하거나 플랫폼 이미지 버전을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-143">It supports changing a platform image version or changing hello URI of a custom image.</span></span>

### <a name="vmsseditor"></a><span data-ttu-id="62b65-144">Vmsseditor</span><span class="sxs-lookup"><span data-stu-id="62b65-144">Vmsseditor</span></span>
<span data-ttu-id="62b65-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) 는 한 행이 하나의 업데이트 도메인을 나타내는 heatmap으로 가상 컴퓨터 상태를 표시하는 가상 컴퓨터 확장 집합에 대한 범용 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) is a general-purpose editor for virtual machine scale sets that shows virtual machine status as a heatmap where one row represents one update domain.</span></span> <span data-ttu-id="62b65-146">특히, 새 버전, SKU 또는 사용자 지정 이미지 URI 크기 집합에 대 한 hello 모델을 업데이트 하 고 오류 도메인 tooupgrade가 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-146">Among other things, you can update hello model for a scale set with a new version, SKU, or custom image URI, and then pick fault domains tooupgrade.</span></span> <span data-ttu-id="62b65-147">이렇게 하면 해당 업데이트 도메인에 있는 모든 hello 가상 컴퓨터는 업그레이드 된 toohello 새 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-147">When you do so, all hello virtual machines in that update domain are upgraded toohello new model.</span></span> <span data-ttu-id="62b65-148">또는 사용자가 선택한 hello 일괄 처리 크기에 따라 롤링 업그레이드를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-148">Alternatively, you can do a rolling upgrade based on hello batch size of your choice.</span></span>  

<span data-ttu-id="62b65-149">hello 다음 스크린샷은 크기 Ubuntu 14.04 2LTS 14.04.201507060 버전에 대 한 집합의 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-149">hello following screenshot shows a model of a scale set for Ubuntu 14.04-2LTS version 14.04.201507060.</span></span> <span data-ttu-id="62b65-150">더 많은 옵션 이후 추가 된 toothis 도구이 스크린샷 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-150">Many more options have been added toothis tool since this screenshot was taken.</span></span>

![Ubuntu 14.04-2LTS에 대한 확장 집합의 Vmsseditor 모델](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

<span data-ttu-id="62b65-152">클릭 한 후 **업그레이드** 차례로 **자세한 정보 얻기**, UD 0의에서 가상 컴퓨터 tooupdate를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="62b65-152">After you click **Upgrade** and then **Get Details**, virtual machines in UD 0 start tooupdate.</span></span>

![진행 중인 업데이트를 보여 주는 Vmsseditor](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)

