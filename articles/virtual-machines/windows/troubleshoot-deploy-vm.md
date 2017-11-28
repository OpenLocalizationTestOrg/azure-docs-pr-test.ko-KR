---
title: "Azure에서 Windows 가상 컴퓨터 배포 문제 해결 | Microsoft Docs"
description: "Azure Resource Manager 배포 모델에서 Windows 가상 컴퓨터 배포 문제를 해결합니다."
services: virtual-machines-windows
documentationcenter: 
author: genlin
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
ms.openlocfilehash: 6800c137097c2803f28dec7365f6d3f2a173b411
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-deploying-windows-virtual-machine-issues-in-azure"></a><span data-ttu-id="bff77-103">Azure에서 Windows 가상 컴퓨터 배포 문제 해결</span><span class="sxs-lookup"><span data-stu-id="bff77-103">Troubleshoot deploying Windows virtual machine issues in Azure</span></span>

<span data-ttu-id="bff77-104">Azure의 VM(가상 컴퓨터) 배포 문제를 해결하려면 일반적인 오류 및 해결 방법에 대한 [주요 문제](#top-issues)를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-104">To troubleshoot virtual machine (VM) deployment issues in Azure, review the [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="bff77-105">이 문서의 어디에서든 도움이 필요한 경우 [MSDN Azure 및 Stack Overflow 포럼](https://azure.microsoft.com/support/forums/)에서 Azure 전문가에게 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-105">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="bff77-106">또는 Azure 기술 지원 인시던트를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="bff77-107">[Azure 지원 사이트](https://azure.microsoft.com/support/options/) 로 가서 **지원 받기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-107">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="bff77-108">주요 문제</span><span class="sxs-lookup"><span data-stu-id="bff77-108">Top issues</span></span>
[!INCLUDE [virtual-machines-windows-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

## <a name="the-cluster-cannot-support-the-requested-vm-size"></a><span data-ttu-id="bff77-109">클러스터가 요청된 VM 크기를 지원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-109">The cluster cannot support the requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="bff77-110">더 작은 VM 크기를 사용하여 요청을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-110">Retry the request using a smaller VM size.</span></span>
- <span data-ttu-id="bff77-111">요청한 VM의 크기를 변경할 수 없으면:</span><span class="sxs-lookup"><span data-stu-id="bff77-111">If the size of the requested VM cannot be changed:</span></span>
    - <span data-ttu-id="bff77-112">가용성 집합의 VM을 모두 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-112">Stop all the VMs in the availability set.</span></span> <span data-ttu-id="bff77-113">**리소스 그룹** > 사용자의 리소스 그룹 > **리소스** > 사용자의 가용성 집합 > **Virtual Machines** > 사용자의 가상 컴퓨터 > **중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="bff77-114">VM을 모두 중지한 후에, 원하는 크기로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-114">After all the VMs stop, create the VM in the desired size.</span></span>
    - <span data-ttu-id="bff77-115">먼저 VM을 시작한 후에 중지된 각각의 VM을 선택하고 시작을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-115">Start the new VM first, and then select each of the stopped VMs and click Start.</span></span>


## <a name="the-cluster-does-not-have-free-resources"></a><span data-ttu-id="bff77-116">클러스터에 여유 리소스가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-116">The cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="bff77-117">요청을 나중에 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="bff77-117">Retry the request later.</span></span>
- <span data-ttu-id="bff77-118">새 VM이 다른 가용성 집합의 일부가 될 수 있다면</span><span class="sxs-lookup"><span data-stu-id="bff77-118">If the new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="bff77-119">동일한 지역의 다른 가용성 집합에 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-119">Create a VM in a different availability set (in the same region).</span></span>
    - <span data-ttu-id="bff77-120">새 VM을 동일한 가상 네트워크에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-120">Add the new VM to the same virtual network.</span></span>

## <a name="how-can-i-use-and-deploy-a-windows-client-image-into-azure"></a><span data-ttu-id="bff77-121">Windows 클라이언트 이미지를 사용하고 Azure에 배포하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="bff77-121">How can I use and deploy a windows client image into Azure?</span></span>

<span data-ttu-id="bff77-122">적절한 Visual Studio(이전의 MSDN) 구독이 있으면 Azure에서 개발/테스트 시나리오에 Windows 7, Windows 8 또는 Windows 10을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-122">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios if you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> <span data-ttu-id="bff77-123">이 [문서](client-images.md)에서는 Azure에서 Windows 클라이언트를 실행하고 Azure 갤러리 이미지를 사용하기 위한 적격성 요구 사항에 대해 대략적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-123">This [article](client-images.md) outlines the eligibility requirements for running Windows client in Azure and uses of the Azure Gallery images.</span></span>

## <a name="how-can-i-deploy-a-virtual-machine-using-the-hybrid-use-benefit-hub"></a><span data-ttu-id="bff77-124">HUB(Hybrid Use Benefit)를 사용하여 가상 컴퓨터를 배포하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="bff77-124">How can I deploy a virtual machine using the Hybrid Use Benefit (HUB)?</span></span>

<span data-ttu-id="bff77-125">Azure 하이브리드 사용 혜택을 사용하여 Windows 가상 컴퓨터를 배포하는 몇 가지 다른 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-125">There are a couple of different ways to deploy Windows virtual machines with the Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="bff77-126">기업 계약 구독의 경우:</span><span class="sxs-lookup"><span data-stu-id="bff77-126">For an Enterprise Agreement subscription:</span></span>

<span data-ttu-id="bff77-127">• Azure 하이브리드 사용 혜택으로 미리 구성되어 있는 특정 Marketplace 이미지에서 VM을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-127">•   Deploy VMs from specific Marketplace images that are pre-configured with Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="bff77-128">기업 계약의 경우:</span><span class="sxs-lookup"><span data-stu-id="bff77-128">For Enterprise agreement:</span></span>

<span data-ttu-id="bff77-129">• 사용자 지정 VM을 업로드하거나 Resource Manager 템플릿 또는 Azure PowerShell을 사용하여 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-129">•   Upload a custom VM and deploy using a Resource Manager template or Azure PowerShell.</span></span>

<span data-ttu-id="bff77-130">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bff77-130">For more information, see the following resources:</span></span>

 - [<span data-ttu-id="bff77-131">Azure Hybrid Use Benefit 개요</span><span class="sxs-lookup"><span data-stu-id="bff77-131">Azure Hybrid Use Benefit overview </span></span>](https://azure.microsoft.com/pricing/hybrid-use-benefit/)

 - [<span data-ttu-id="bff77-132">다운로드 가능한 FAQ</span><span class="sxs-lookup"><span data-stu-id="bff77-132">Downloadable FAQ</span></span>](http://download.microsoft.com/download/4/2/1/4211AC94-D607-4A45-B472-4B30EDF437DE/Windows_Server_Azure_Hybrid_Use_FAQ_EN_US.pdf)

 - <span data-ttu-id="bff77-133">[Window Server 및 Windows 클라이언트용 Azure Hybrid Use Benefit](hybrid-use-benefit-licensing.md)</span><span class="sxs-lookup"><span data-stu-id="bff77-133">[Azure Hybrid Use Benefit for Windows Server and Windows Client](hybrid-use-benefit-licensing.md).</span></span>

 - [<span data-ttu-id="bff77-134">Azure에서 Hybrid Use Benefit을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="bff77-134">How can I use the Hybrid Use Benefit in Azure</span></span>](https://blogs.msdn.microsoft.com/azureedu/2016/04/13/how-can-i-use-the-hybrid-use-benefit-in-azure)

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="bff77-135">Visual Studio Enterprise(BizSpark)에 대한 월간 크레딧을 활성화하는 방법</span><span class="sxs-lookup"><span data-stu-id="bff77-135">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="bff77-136">월별 크레딧을 활성화하려면 이 [문서](https://azure.microsoft.com/offers/ms-azr-0064p/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bff77-136">To activate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="how-to-add-enterprise-devtest-to-my-enterprise-agreement-ea-to-get-access-to-window-client-images"></a><span data-ttu-id="bff77-137">내 EA(기업 계약)에 Enterprise 개발/테스트를 추가하여 Windows 클라이언트 이미지에 액세스하는 방법</span><span class="sxs-lookup"><span data-stu-id="bff77-137">How to add Enterprise Dev/Test to my Enterprise Agreement (EA) to get access to Window client images?</span></span>

<span data-ttu-id="bff77-138">Enterprise 개발/테스트 제품을 기준으로 구독을 생성하는 작업은 엔터프라이즈 관리자에게 그러한 권한을 받은 계정 소유자만 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-138">The ability to create subscriptions based on the Enterprise Dev/Test offer is restricted to Account Owners who have been given permission to do so by an Enterprise Administrator.</span></span> <span data-ttu-id="bff77-139">계정 소유자는 Azure 계정 포털을 통해 구독을 생성한 다음 Visual Studio 활성 구독자를 공동 관리자로 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-139">The Account Owner creates subscriptions via the Azure Account Portal, and then should add active Visual Studio subscribers as co-administrators.</span></span> <span data-ttu-id="bff77-140">그러면 개발 및 테스트에 필요한 리소스를 관리하고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-140">So that they can manage and use the resources needed for development and testing.</span></span> <span data-ttu-id="bff77-141">자세한 내용은 [Enterprise 개발/테스트](https://azure.microsoft.com/offers/ms-azr-0148p/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bff77-141">For more information, see [Enterprise Dev/Test](https://azure.microsoft.com/offers/ms-azr-0148p/).</span></span>

## <a name="my-drivers-are-missing-for-my-windows-n-series-vm"></a><span data-ttu-id="bff77-142">내 드라이버가 Windows N 시리즈 VM에 누락되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-142">My drivers are missing for my Windows N-Series VM</span></span>

<span data-ttu-id="bff77-143">Windows 기반 VM용 드라이버가 [여기](n-series-driver-setup.md)에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-143">Drivers for Windows-based VMs are located [here](n-series-driver-setup.md).</span></span>

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="bff77-144">N 시리즈 VM 내에서 GPU 인스턴스를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-144">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="bff77-145">Windows Server 2016 또는 Windows Server 2012 R2를 실행하는 Azure N 시리즈 VM의 GPU 기능을 이용하려면 배포 후 각 VM에 NVIDIA 그래픽 드라이버를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-145">To take advantage of the GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="bff77-146">[Windows VM](n-series-driver-setup.md) 및 [Linux VM](../linux/n-series-driver-setup.md)에 대한 드라이버 설치 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-146">Driver setup information is available for [Windows VMs](n-series-driver-setup.md) and [Linux VMs](../linux/n-series-driver-setup.md).</span></span>

## <a name="are-client-images-supported-for-n-series"></a><span data-ttu-id="bff77-147">클라이언트 이미지가 N 시리즈에 지원되나요?</span><span class="sxs-lookup"><span data-stu-id="bff77-147">Are client images supported for N-Series?</span></span>

<span data-ttu-id="bff77-148">현재 Azure는 Windows Server 및 Linux 운영 체제를 실행하는 VM에서만 N 시리즈를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-148">Currently, Azure only supports N-Series on VMs running Windows Server and Linux operating systems.</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="bff77-149">N 시리즈 VM을 내 지역에서 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="bff77-149">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="bff77-150">가용성을 [지역에서 사용할 수 있는 제품 표](https://azure.microsoft.com/regions/services)에서 확인할 수 있고 가격 책정을 [여기](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-150">You can check the availability from the [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="what-client-images-can-i-use-and-deploy-in-azure-and-how-to-i-get-them"></a><span data-ttu-id="bff77-151">어떤 클라이언트 이미지를 사용하여 Azure에 배포하고 어떻게 가져올 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="bff77-151">What client images can I use and deploy in Azure, and how to I get them?</span></span>

<span data-ttu-id="bff77-152">적절한 Visual Studio(이전의 MSDN) 구독이 있으면 Azure에서 개발/테스트 시나리오에 Windows 7, Windows 8 또는 Windows 10을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-152">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios provided you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> 

- <span data-ttu-id="bff77-153">[적격 개발/테스트 제품](client-images.md#eligible-offers) 내에서 Azure 갤러리의 특정 Windows 10 이미지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-153">Windows 10 images are available from the Azure Gallery within [eligible dev/test offers](client-images.md#eligible-offers).</span></span> 
- <span data-ttu-id="bff77-154">Visual Studio 구독자(사용 중인 제품 유형은 관계없음)는 64비트 Windows 7, Windows 8 또는 Windows 10 이미지를 [적절하게 준비하고 작성](prepare-for-upload-vhd-image.md)한 다음 [Azure에 업로드](upload-generalized-managed.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-154">Visual Studio subscribers within any type of offer can also [adequately prepare and create](prepare-for-upload-vhd-image.md) a 64-bit Windows 7, Windows 8, or Windows 10 image and then [upload to Azure](upload-generalized-managed.md).</span></span> <span data-ttu-id="bff77-155">이렇게 업로드하는 이미지 역시 활성 Visual Studio 구독자가 개발/테스트용으로만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-155">The use remains limited to dev/test by active Visual Studio subscribers.</span></span>

<span data-ttu-id="bff77-156">이 [문서](client-images.md)에서는 Azure에서 Windows 클라이언트를 실행하고 Azure 갤러리 이미지를 사용하기 위한 적격성 요구 사항에 대해 대략적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-156">This [article](client-images.md) outlines the eligibility requirements for running Windows client in Azure and use of the Azure Gallery images.</span></span>

## <a name="i-am-not-able-to-see-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="bff77-157">VM 크기를 조정할 때 원하는 VM 크기 제품군이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-157">I am not able to see VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="bff77-158">VM을 실행하면 해당 VM이 실제 서버에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-158">When a VM is running, it is deployed to a physical server.</span></span> <span data-ttu-id="bff77-159">Azure 지역의 물리적 서버는 일반적인 실제 하드웨어의 클러스터에서 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-159">The physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="bff77-160">VM을 다른 하드웨어 클러스터에 이동해야 하는 VM 크기 조정은 VM을 배포하는 데 사용되는 배포 모델에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-160">Resizing a VM that requires the VM to be moved to different hardware clusters is different depending on which deployment model was used to deploy the VM.</span></span>

- <span data-ttu-id="bff77-161">클래식 배포 모델에서 배포된 VM의 경우 클라우드 서비스 배포를 제거하고 다시 배포하여 다른 크기 제품군의 크기로 VM을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-161">VMs deployed in Classic deployment model, the cloud service deployment must be removed and redeployed to change the VMs to a size in another size family.</span></span>

- <span data-ttu-id="bff77-162">Resource Manager 배포 모델에서 배포된 VM의 경우 가용성 집합에 있는 VM의 크기를 변경하기 전에 모든 VM을 중지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-162">VMs deployed in Resource Manager deployment model, you must stop all VMs in the availability set before changing the size of any VM in the availability set.</span></span>

## <a name="the-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="bff77-163">가용성 집합에서 배포하는 동안 나열된 VM 크기는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-163">The listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="bff77-164">가용성 집합의 클러스터에서 지원되는 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-164">Choose a size that is supported on the availability set's cluster.</span></span> <span data-ttu-id="bff77-165">가용성 집합을 만들 때 필요할 수 있는 가장 큰 VM 크기를 선택하고 가용성 집합에 첫 번째로 배포하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-165">It is recommended when creating an availability set to choose the largest VM size you think you need, and have that be your first deployment to the Availability set.</span></span>

## <a name="can-i-add-an-existing-classic-vm-to-an-availability-set"></a><span data-ttu-id="bff77-166">가용성 집합에 기존 클래식 VM을 추가할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="bff77-166">Can I add an existing Classic VM to an availability set?</span></span>

<span data-ttu-id="bff77-167">예.</span><span class="sxs-lookup"><span data-stu-id="bff77-167">Yes.</span></span> <span data-ttu-id="bff77-168">새 가용성 집합 또는 기존 가용성 집합에 기존 클래식 VM을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-168">You can add an existing classic VM to a new or existing Availability Set.</span></span> <span data-ttu-id="bff77-169">자세한 내용은 [가용성 집합에 기존 가상 컴퓨터 추가](classic/configure-availability.md#addmachine)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bff77-169">For more information see [Add an existing virtual machine to an availability set](classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="bff77-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bff77-170">Next steps</span></span>
<span data-ttu-id="bff77-171">이 문서의 어디에서든 도움이 필요한 경우 [MSDN Azure 및 Stack Overflow 포럼](https://azure.microsoft.com/support/forums/)에서 Azure 전문가에게 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-171">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="bff77-172">또는 Azure 기술 지원 인시던트를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-172">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="bff77-173">[Azure 지원 사이트](https://azure.microsoft.com/support/options/) 로 가서 **지원 받기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bff77-173">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
