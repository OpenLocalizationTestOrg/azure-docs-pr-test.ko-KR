---
title: "Linux VM 배포 클래식 문제 해결 | Microsoft Docs"
description: "Azure에서 새 Linux 가상 컴퓨터를 만드는 경우 클래식 배포 문제 해결"
services: virtual-machines-linux
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: c8a963fa-6b2a-4c7a-a1f4-7793adb02b19
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cjiang
ms.openlocfilehash: 35b8ae033425e16fb53cc3127f300e1fb919a2f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a><span data-ttu-id="c68c8-103">Azure에서 새 Linux 가상 컴퓨터 생성 관련 클래식 배포 문제 해결</span><span class="sxs-lookup"><span data-stu-id="c68c8-103">Troubleshoot classic deployment issues with creating a new Linux virtual machine in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-selectors](../../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-selectors-include.md)]

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

> [!IMPORTANT] 
> <span data-ttu-id="c68c8-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c68c8-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="c68c8-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="c68c8-107">이 문서의 Resource Manager 버전은 [여기](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c68c8-107">For the Resource Manager version of this article, see [here](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="c68c8-108">감사 로그 수집</span><span class="sxs-lookup"><span data-stu-id="c68c8-108">Collect audit logs</span></span>
<span data-ttu-id="c68c8-109">문제 해결을 시작하려면 문제와 관련된 오류를 파악하기 위해 감사 로그를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-109">To start troubleshooting, collect the audit logs to identify the error associated with the issue.</span></span>

<span data-ttu-id="c68c8-110">Azure 포털에서 **찾아보기** > **가상 컴퓨터** > *Windows 가상 컴퓨터* > **설정** > **감사 로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-110">In the Azure portal, click **Browse** > **Virtual machines** > *your Windows virtual machine* > **Settings** > **Audit logs**.</span></span>

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="c68c8-111">**Y:** OS가 일반화된 Linux인 경우, 일반화된 설정을 사용하여 업로드되거나 캡처되고, 오류는 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-111">**Y:** If the OS is Linux generalized, and it is uploaded and/or captured with the generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="c68c8-112">마찬가지로 OS가 특수화된 Linux인 경우, 특수화된 설정을 사용하여 업로드되거나 캡처되고, 오류는 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-112">Similarly, if the OS is Linux specialized, and it is uploaded and/or captured with the specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="c68c8-113">**업로드 오류:**</span><span class="sxs-lookup"><span data-stu-id="c68c8-113">**Upload Errors:**</span></span>

<span data-ttu-id="c68c8-114">**N<sup>1</sup>:** OS가 일반화된 Linux이고 특수화된 것으로 업로드된다면, VM이 프로비전 단계에서 중단되기 때문에 프로비전 시간 초과 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-114">**N<sup>1</sup>:** If the OS is Linux generalized, and it is uploaded as specialized, you will get a provisioning timeout error because the VM is stuck at the provisioning stage.</span></span>

<span data-ttu-id="c68c8-115">**N<sup>2</sup>:** OS가 특수화된 Linux이고 일반화된 것으로 업로드된다면, 새 VM이 원래 컴퓨터 이름, 사용자 이름 및 암호로 실행되기 때문에 프로비전 실패 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-115">**N<sup>2</sup>:** If the OS is Linux specialized, and it is uploaded as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username and password.</span></span>

<span data-ttu-id="c68c8-116">**해결 방법:**</span><span class="sxs-lookup"><span data-stu-id="c68c8-116">**Resolution:**</span></span>

<span data-ttu-id="c68c8-117">이 두 가지 오류를 모두 해결하려면, 온-프레미스에 있는 원본 VHD를, OS와 같은 설정(일반화/특수화)으로 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-117">To resolve both these errors, upload the original VHD, available on-prem, with the same setting as that for the OS (generalized/specialized).</span></span> <span data-ttu-id="c68c8-118">일반화된 것으로 업로드하려면, 먼저 프로비전 해제를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-118">To upload as generalized, remember to run -deprovision first.</span></span> <span data-ttu-id="c68c8-119">자세한 내용은 [Linux 운영 체제를 포함한 가상 하드 디스크 만들기 및 업로드](create-upload-vhd.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c68c8-119">See [Create and Upload a Virtual Hard Disk that Contains the Linux Operating System](create-upload-vhd.md) for more information.</span></span>

<span data-ttu-id="c68c8-120">**캡처 오류:**</span><span class="sxs-lookup"><span data-stu-id="c68c8-120">**Capture Errors:**</span></span>

<span data-ttu-id="c68c8-121">**N<sup>3</sup>:** OS가 일반화된 Linux이고 특수화된 것으로 캡처된다면, 원본 VM이 일반화된 것으로 표시되어 사용할 수 없기 때문에 프로비전 시간 초과 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-121">**N<sup>3</sup>:** If the OS is Linux generalized, and it is captured as specialized, you will get a provisioning timeout error because the original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="c68c8-122">**N<sup>4</sup>:** OS가 특수화된 Linux이고 일반화된 것으로 캡처된다면, 새 VM이 원래 컴퓨터 이름, 사용자 이름 및 암호로 실행되기 때문에 프로비전 실패 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-122">**N<sup>4</sup>:** If the OS is Linux specialized, and it is captured as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username and password.</span></span> <span data-ttu-id="c68c8-123">또한, 원본 VM이 일반화된 것으로 표시되기 때문에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-123">Also, the original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="c68c8-124">**해결 방법:**</span><span class="sxs-lookup"><span data-stu-id="c68c8-124">**Resolution:**</span></span>

<span data-ttu-id="c68c8-125">이 두 가지 오류를 모두 해결하려면, 현재 이미지를 포털에서 제거하고, OS와 같은 설정(일반화/특수화)으로 [현재 VHD에서 다시 캡처](capture-image.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-125">To resolve both these errors, delete the current image from the portal, and [recapture it from the current VHDs](capture-image.md) with the same setting as that for the OS (generalized/specialized).</span></span>

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a><span data-ttu-id="c68c8-126">문제: 사용자 지정/ 갤러리/ 마켓플레이스 이미지; 할당 오류</span><span class="sxs-lookup"><span data-stu-id="c68c8-126">Issue: Custom/ gallery/ marketplace image; allocation failure</span></span>
<span data-ttu-id="c68c8-127">이 오류는 요청을 수용할 여유 공간이 없거나 요청되는 VM 크기를 지원할 수 없는 클러스터로 새 VM 요청이 전송된 상황에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-127">This error arises in situations when the new VM request is sent to a cluster that either does not have available free space to accommodate the request, or cannot support the VM size being requested.</span></span> <span data-ttu-id="c68c8-128">동일한 클라우드 서비스에 일련의 다른 VM을 혼합하는 것은 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-128">It is not possible to mix different series of VMs in the same cloud service.</span></span> <span data-ttu-id="c68c8-129">따라서 클라우드 서비스에서 지원할 수 있는 것과 다른 크기의 VM을 새로 만들려고 하면, 계산 요청이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-129">So if you want to create a new VM of a different size than what your cloud service can support, the compute request will fail.</span></span>

<span data-ttu-id="c68c8-130">새 VM을 만드는 데 사용한 클라우드 서비스의 제약 조건에 따라서, 둘 중 한가지 상황에 의해 유발되는 오류를 접하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-130">Depending on the constraints of the cloud service you use to create the new VM, you might encounter an error caused by one of two situations.</span></span>

<span data-ttu-id="c68c8-131">**원인 1:** 클라우드 서비스가 특정 클러스터에 고정되어 있거나, 선호도 그룹에 연결되어 있기 때문에, 의도적으로 특정 클러스터에 고정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-131">**Cause 1:** The cloud service is pinned to a specific cluster, or it is linked to an affinity group, and hence pinned to a specific cluster by design.</span></span> <span data-ttu-id="c68c8-132">선호도 그룹의 새로운 계산 리소스 요청이 기존 리소스가 호스트된 동일한 클러스터에서 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-132">So new compute resource requests in that affinity group are tried in the same cluster where the existing resources are hosted.</span></span> <span data-ttu-id="c68c8-133">하지만, 동일한 클러스터가 요청된 VM 크기를 지원하지 않거나 사용할 수 있는 공간이 부족하여 할당 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-133">However, the same cluster may either not support the requested VM size or have insufficient available space, resulting in an allocation error.</span></span> <span data-ttu-id="c68c8-134">새로운 리소스가 새 클라우드 서비스에서 만들어지건 아니면 기존 클라우드 서비스를 통해 만들어지건 이 내용은 사실입니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-134">This is true whether the new resources are created through a new cloud service or through an existing cloud service.</span></span>

<span data-ttu-id="c68c8-135">**해결 방법 1:**</span><span class="sxs-lookup"><span data-stu-id="c68c8-135">**Resolution 1:**</span></span>

* <span data-ttu-id="c68c8-136">새 클라우드 서비스를 만들어서 지역 또는 지역 기반 가상 네트워크와 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-136">Create a new cloud service and associate it with either a region or a region-based virtual network.</span></span>
* <span data-ttu-id="c68c8-137">새 클라우드 서비스에 새 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-137">Create a new VM in the new cloud service.</span></span>
  <span data-ttu-id="c68c8-138">새 클라우드 서비스를 만들려다 오류가 발생하면, 나중에 다시 시도하거나 클라우드 서비스의 지역을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-138">If you get an error when trying to create a new cloud service, either retry at a later time or change the region for the cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c68c8-139">기존 클라우드 서비스에 새 VM을 만들려다 실패했고, 새 VM을 위해 새 클라우드 서비스를 만들어야 한다면, 모든 VM을 동일한 클라우드 서비스에 통합하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-139">If you were trying to create a new VM in an existing cloud service but couldn’t, and had to create a new cloud service for your new VM, you can choose to consolidate all your VMs in the same cloud service.</span></span> <span data-ttu-id="c68c8-140">이렇게 하려면, 기존 클라우드 서비스의 VM을 삭제하고, 새 클라우드 서비스의 디스크에서 VM을 다시 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-140">To do so, delete the VMs in the existing cloud service, and recapture them from their disks in the new cloud service.</span></span> <span data-ttu-id="c68c8-141">하지만, 새 클라우드 서비스가 새 이름과 VIP를 갖게 되므로, 기존 클라우드 서비스에 이 정보를 사용하는 모든 종속성에 대해 해당 정보를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-141">However, it is important to remember that the new cloud service will have a new name and VIP, so you will need to update these for all the dependencies that currently use this information for the existing cloud service.</span></span>
> 
> 

<span data-ttu-id="c68c8-142">**원인 2:** 클라우드 서비스가 선호도 그룹에 연결된 가상 네트워크와 연결되어 있어서, 의도적으로 특정 클러스터에 고정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-142">**Cause 2:** The cloud service is associated with a virtual network that is linked to an affinity group, so it is pinned to a specific cluster by design.</span></span> <span data-ttu-id="c68c8-143">따라서 선호도 그룹의 모든 새로운 계산 리소스 요청이 기존 리소스가 호스트된 동일한 클러스터에서 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-143">All new compute resource requests in that affinity group are therefore tried in the same cluster where the existing resources are hosted.</span></span> <span data-ttu-id="c68c8-144">하지만, 동일한 클러스터가 요청된 VM 크기를 지원하지 않거나 사용할 수 있는 공간이 부족하여 할당 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-144">However, the same cluster may either not support the requested VM size or have insufficient available space, resulting in an allocation error.</span></span> <span data-ttu-id="c68c8-145">새로운 리소스가 새 클라우드 서비스에서 만들어지건 아니면 기존 클라우드 서비스를 통해 만들어지건 이 내용은 사실입니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-145">This is true whether the new resources are created through a new cloud service or through an existing cloud service.</span></span>

<span data-ttu-id="c68c8-146">**해결 방법 2:**</span><span class="sxs-lookup"><span data-stu-id="c68c8-146">**Resolution 2:**</span></span>

* <span data-ttu-id="c68c8-147">새 지역 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-147">Create a new regional virtual network.</span></span>
* <span data-ttu-id="c68c8-148">새 가상 네트워크에 새 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-148">Create the new VM in the new virtual network.</span></span>
* <span data-ttu-id="c68c8-149">[기존 가상 네트워크를 연결](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/) 합니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-149">[Connect your existing virtual network](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/) to the new virtual network.</span></span> <span data-ttu-id="c68c8-150">[지역 가상 네트워크](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/)에 대한 자세한 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c68c8-150">See more about [regional virtual networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).</span></span> <span data-ttu-id="c68c8-151">또는 [선호도 그룹 기반 가상 네트워크를 지역 가상 네트워크로 마이그레이션](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/)한 다음 새 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c68c8-151">Alternatively, you can [migrate your affinity-group-based virtual network to a regional virtual network](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/), and then create the new VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c68c8-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c68c8-152">Next steps</span></span>
<span data-ttu-id="c68c8-153">중지된 Linux VM을 시작하거나 Azure에서 기존 Linux VM의 크기를 조정할 때 문제가 발생하면 [Azure의 기존 Linux 가상 컴퓨터 재시작 또는 크기 조정 관련 클래식 배포 문제 해결](restart-resize-error-troubleshooting.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c68c8-153">If you encounter issues when you start a stopped Linux VM or resize an existing Linux VM in Azure, see [Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure](restart-resize-error-troubleshooting.md).</span></span>

