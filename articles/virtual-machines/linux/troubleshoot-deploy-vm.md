---
title: "Azure에서 Linux 가상 컴퓨터 배포 문제 해결 | Microsoft Docs"
description: "Azure Resource Manager 배포 모델에서 Linux 가상 컴퓨터 배포 문제를 해결합니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: genli
ms.openlocfilehash: 8bc9de90a49caf9155073caaa160585c6cc3728b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a><span data-ttu-id="b649d-103">Azure에서 Linux 가상 컴퓨터 배포 문제 해결</span><span class="sxs-lookup"><span data-stu-id="b649d-103">Troubleshoot deploying Linux virtual machine issues in Azure</span></span>

<span data-ttu-id="b649d-104">Azure의 VM(가상 컴퓨터) 배포 문제를 해결하려면 일반적인 오류 및 해결 방법에 대한 [주요 문제](#top-issues)를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-104">To troubleshoot virtual machine (VM) deployment issues in Azure, review the [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="b649d-105">이 문서의 어디에서든 도움이 필요한 경우 [MSDN Azure 및 Stack Overflow 포럼](https://azure.microsoft.com/support/forums/)에서 Azure 전문가에게 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-105">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="b649d-106">또는 Azure 기술 지원 인시던트를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="b649d-107">[Azure 지원 사이트](https://azure.microsoft.com/support/options/) 로 가서 **지원 받기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-107">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="b649d-108">주요 문제</span><span class="sxs-lookup"><span data-stu-id="b649d-108">Top issues</span></span>
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="the-cluster-cannot-support-the-requested-vm-size"></a><span data-ttu-id="b649d-109">클러스터가 요청된 VM 크기를 지원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-109">The cluster cannot support the requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="b649d-110">더 작은 VM 크기를 사용하여 요청을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-110">Retry the request using a smaller VM size.</span></span>
- <span data-ttu-id="b649d-111">요청한 VM의 크기를 변경할 수 없으면:</span><span class="sxs-lookup"><span data-stu-id="b649d-111">If the size of the requested VM cannot be changed:</span></span>
    - <span data-ttu-id="b649d-112">가용성 집합의 VM을 모두 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-112">Stop all the VMs in the availability set.</span></span> <span data-ttu-id="b649d-113">**리소스 그룹** > 사용자의 리소스 그룹 > **리소스** > 사용자의 가용성 집합 > **Virtual Machines** > 사용자의 가상 컴퓨터 > **중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="b649d-114">VM을 모두 중지한 후에, 원하는 크기로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-114">After all the VMs stop, create the VM in the desired size.</span></span>
    - <span data-ttu-id="b649d-115">먼저 VM을 시작한 후에 중지된 각각의 VM을 선택하고 시작을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-115">Start the new VM first, and then select each of the stopped VMs and click Start.</span></span>


## <a name="the-cluster-does-not-have-free-resources"></a><span data-ttu-id="b649d-116">클러스터에 여유 리소스가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-116">The cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="b649d-117">요청을 나중에 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="b649d-117">Retry the request later.</span></span>
- <span data-ttu-id="b649d-118">새 VM이 다른 가용성 집합의 일부가 될 수 있다면</span><span class="sxs-lookup"><span data-stu-id="b649d-118">If the new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="b649d-119">동일한 지역의 다른 가용성 집합에 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-119">Create a VM in a different availability set (in the same region).</span></span>
    - <span data-ttu-id="b649d-120">새 VM을 동일한 가상 네트워크에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-120">Add the new VM to the same virtual network.</span></span>

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="b649d-121">Visual Studio Enterprise(BizSpark)에 대한 월간 크레딧을 활성화하는 방법</span><span class="sxs-lookup"><span data-stu-id="b649d-121">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="b649d-122">월별 크레딧을 활성화하려면 이 [문서](https://azure.microsoft.com/offers/ms-azr-0064p/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b649d-122">To activate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="why-can-i-not-install-the-gpu-driver-for-an-ubuntu-nv-vm"></a><span data-ttu-id="b649d-123">Ubuntu NV VM에 GPU 드라이버를 설치할 수 없는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="b649d-123">Why can I not install the GPU driver for an Ubuntu NV VM?</span></span>

<span data-ttu-id="b649d-124">현재 Linux GPU 지원은 Ubuntu Server 16.04 LTS를 실행하는 Azure NC VM에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-124">Currently, Linux GPU support is only available on Azure NC VMs running Ubuntu Server 16.04 LTS.</span></span> <span data-ttu-id="b649d-125">자세한 내용은 [Linux가 실행되는 N 시리즈 VM의 GPU 드라이버 설정](n-series-driver-setup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b649d-125">For more information, see [Set up GPU drivers for N-series VMs running Linux](n-series-driver-setup.md).</span></span>

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a><span data-ttu-id="b649d-126">내 드라이버가 Linux N 시리즈 VM에 누락되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-126">My drivers are missing for my Linux N-Series VM</span></span>

<span data-ttu-id="b649d-127">Linux 기반 VM용 드라이버가 [여기](n-series-driver-setup.md)에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-127">Drivers for Linux-based VMs are located [here](n-series-driver-setup.md).</span></span> 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="b649d-128">N 시리즈 VM 내에서 GPU 인스턴스를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-128">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="b649d-129">Windows Server 2016 또는 Windows Server 2012 R2를 실행하는 Azure N 시리즈 VM의 GPU 기능을 이용하려면 배포 후 각 VM에 NVIDIA 그래픽 드라이버를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-129">To take advantage of the GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="b649d-130">[Windows VM](../windows/n-series-driver-setup.md) 및 [Linux VM](n-series-driver-setup.md)에 대한 드라이버 설치 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-130">Driver setup information is available for [Windows VMs](../windows/n-series-driver-setup.md) and [Linux VMs](n-series-driver-setup.md).</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="b649d-131">N 시리즈 VM을 내 지역에서 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="b649d-131">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="b649d-132">가용성을 [지역에서 사용할 수 있는 제품 표](https://azure.microsoft.com/regions/services)에서 확인할 수 있고 가격 책정을 [여기](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-132">You can check the availability from the [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="i-am-not-able-to-see-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="b649d-133">VM 크기를 조정할 때 원하는 VM 크기 제품군이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-133">I am not able to see VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="b649d-134">VM을 실행하면 해당 VM이 실제 서버에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-134">When a VM is running, it is deployed to a physical server.</span></span> <span data-ttu-id="b649d-135">Azure 지역의 물리적 서버는 일반적인 실제 하드웨어의 클러스터에서 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-135">The physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="b649d-136">VM을 다른 하드웨어 클러스터에 이동해야 하는 VM 크기 조정은 VM을 배포하는 데 사용되는 배포 모델에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-136">Resizing a VM that requires the VM to be moved to different hardware clusters is different depending on which deployment model was used to deploy the VM.</span></span>

- <span data-ttu-id="b649d-137">클래식 배포 모델에서 배포된 VM의 경우 클라우드 서비스 배포를 제거하고 다시 배포하여 다른 크기 제품군의 크기로 VM을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-137">VMs deployed in Classic deployment model, the cloud service deployment must be removed and redeployed to change the VMs to a size in another size family.</span></span>

- <span data-ttu-id="b649d-138">Resource Manager 배포 모델에서 배포된 VM의 경우 가용성 집합에 있는 VM의 크기를 변경하기 전에 모든 VM을 중지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-138">VMs deployed in Resource Manager deployment model, you must stop all VMs in the availability set before changing the size of any VM in the availability set.</span></span>

## <a name="the-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="b649d-139">가용성 집합에서 배포하는 동안 나열된 VM 크기는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-139">The listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="b649d-140">가용성 집합의 클러스터에서 지원되는 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-140">Choose a size that is supported on the availability set's cluster.</span></span> <span data-ttu-id="b649d-141">가용성 집합을 만들 때 필요할 수 있는 가장 큰 VM 크기를 선택하고 가용성 집합에 첫 번째로 배포하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-141">It is recommended when creating an availability set to choose the largest VM size you think you need, and have that be your first deployment to the Availability set.</span></span>

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a><span data-ttu-id="b649d-142">Azure에서 지원되는 Linux 배포/버전은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="b649d-142">What Linux distributions/versions are supported on Azure?</span></span>

<span data-ttu-id="b649d-143">[Azure 인증 배포](endorsed-distros.md)에 대한 Linux 목록을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-143">You can find the list at Linux on [Azure-Endorsed Distributions](endorsed-distros.md).</span></span>

## <a name="can-i-add-an-existing-classic-vm-to-an-availability-set"></a><span data-ttu-id="b649d-144">가용성 집합에 기존 클래식 VM을 추가할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="b649d-144">Can I add an existing Classic VM to an availability set?</span></span>

<span data-ttu-id="b649d-145">예.</span><span class="sxs-lookup"><span data-stu-id="b649d-145">Yes.</span></span> <span data-ttu-id="b649d-146">새 가용성 집합 또는 기존 가용성 집합에 기존 클래식 VM을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-146">You can add an existing classic VM to a new or existing Availability Set.</span></span> <span data-ttu-id="b649d-147">자세한 내용은 [가용성 집합에 기존 가상 컴퓨터 추가](../windows/classic/configure-availability.md#addmachine)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b649d-147">For more information see [Add an existing virtual machine to an availability set](../windows/classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="b649d-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b649d-148">Next steps</span></span>
<span data-ttu-id="b649d-149">이 문서의 어디에서든 도움이 필요한 경우 [MSDN Azure 및 Stack Overflow 포럼](https://azure.microsoft.com/support/forums/)에서 Azure 전문가에게 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-149">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="b649d-150">또는 Azure 기술 지원 인시던트를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-150">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="b649d-151">[Azure 지원 사이트](https://azure.microsoft.com/support/options/) 로 가서 **지원 받기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b649d-151">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
