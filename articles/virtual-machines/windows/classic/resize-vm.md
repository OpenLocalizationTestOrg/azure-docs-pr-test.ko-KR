---
title: "클래식 배포 모델에서 Windows VM 크기 조정 - Azure | Microsoft Docs"
description: "Azure Powershell을 사용하여 클래식 배포 모델에서 만든 Windows 가상 컴퓨터의 크기를 조정합니다."
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e3038215-001c-406e-904d-e0f4e326a4c7
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: 4277bc8394c7ba140291e9dc776162e87deab96b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="resize-a-windows-vm-created-in-the-classic-deployment-model"></a><span data-ttu-id="fc084-103">클래식 배포 모델에서 만든 Windows VM 크기 조정</span><span class="sxs-lookup"><span data-stu-id="fc084-103">Resize a Windows VM created in the classic deployment model</span></span>
<span data-ttu-id="fc084-104">이 문서에서는 Azure Powershell을 사용하여 클래식 배포 모델에서 만든 Windows VM의 크기를 조정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-104">This article shows you how to resize a Windows VM, created in the classic deployment model using Azure Powershell.</span></span>

<span data-ttu-id="fc084-105">VM의 크기를 조정하는 기능을 고려할 때, 가상 컴퓨터 크기 조정에 사용할 수 있는 크기의 범위를 제어하는 두 가지 개념이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-105">When considering the ability to resize a VM, there are two concepts which control the range of sizes available to resize the virtual machine.</span></span> <span data-ttu-id="fc084-106">첫 번째 개념은 VM이 배포된 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-106">The first concept is the region in which your VM is deployed.</span></span> <span data-ttu-id="fc084-107">지역에 사용할 수 있는 VM 크기 목록은 Azure 지역 웹 페이지의 서비스 탭 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-107">The list of VM sizes available in region is under the Services tab of the Azure Regions web page.</span></span> <span data-ttu-id="fc084-108">두 번째 개념은 현재 VM을 호스팅하는 실제 하드웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-108">The second concept is the physical hardware currently hosting your VM.</span></span> <span data-ttu-id="fc084-109">VM을 호스팅하는 물리적 서버는 일반적인 실제 하드웨어의 클러스터에서 함께 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-109">The physical servers hosting VMs are grouped together in clusters of common physical hardware.</span></span> <span data-ttu-id="fc084-110">VM 크기를 변경하는 방법은 현재 VM을 호스팅하는 하드웨어 클러스터에서 원하는 새 VM 크기를 지원하는지 여부에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-110">The method of changing a VM size differs depending on if the desired new VM size is supported by the hardware cluster currently hosting the VM.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="fc084-111">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fc084-112">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-112">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="fc084-113">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-113">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="fc084-114">[Resource Manager 배포 모델에서 만든 VM의 크기를 조정](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-114">You can also [resize a VM created in the Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="add-your-account"></a><span data-ttu-id="fc084-115">사용자 계정 추가</span><span class="sxs-lookup"><span data-stu-id="fc084-115">Add your account</span></span>
<span data-ttu-id="fc084-116">클래식 Azure 리소스와 함께 작동하도록 Azure PowerShell을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-116">You must configure Azure PowerShell to work with classic Azure resources.</span></span> <span data-ttu-id="fc084-117">클래식 리소스를 관리하도록 Azure PowerShell을 구성하려면 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-117">Follow the steps below to configure Azure PowerShell to manage classic resources.</span></span>

1. <span data-ttu-id="fc084-118">PowerShell 프롬프트에서 `Add-AzureAccount`를 입력하고 **Enter**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-118">At the PowerShell prompt, type `Add-AzureAccount` and click **Enter**.</span></span> 
2. <span data-ttu-id="fc084-119">Azure 구독과 연관된 메일 주소를 입력하고 **계속**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-119">Type in the email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="fc084-120">계정에 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-120">Type in the password for your account.</span></span> 
4. <span data-ttu-id="fc084-121">**로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-121">Click **Sign in**.</span></span> 

## <a name="resize-in-the-same-hardware-cluster"></a><span data-ttu-id="fc084-122">동일한 하드웨어 클러스터에서 크기 조정</span><span class="sxs-lookup"><span data-stu-id="fc084-122">Resize in the same hardware cluster</span></span>
<span data-ttu-id="fc084-123">VM을 호스팅하는 하드웨어 클러스터에서 사용할 수 있는 크기로 VM 크기를 조정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-123">To resize a VM to a size available in the hardware cluster hosting the VM, perform the following steps.</span></span>

1. <span data-ttu-id="fc084-124">VM을 포함하는 클라우드 서비스를 호스팅하는 하드웨어 클러스터에서 사용 가능한 VM 크기를 나열하려면 다음 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-124">Run the following PowerShell command to list the VM sizes available in the hardware cluster hosting the cloud service which contains the VM.</span></span>
   
    ```powershell
    Get-AzureService | where {$_.ServiceName -eq "<cloudServiceName>"}
    ```
2. <span data-ttu-id="fc084-125">다음 명령을 실행하여 VM 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-125">Run the following commands to resize the VM.</span></span>
   
    ```powershell
    Get-AzureVM -ServiceName <cloudServiceName> -Name <vmName> | Set-AzureVMSize -InstanceSize <newVMSize> | Update-AzureVM
    ```

## <a name="resize-on-a-new-hardware-cluster"></a><span data-ttu-id="fc084-126">새 하드웨어 클러스터에서 크기 조정</span><span class="sxs-lookup"><span data-stu-id="fc084-126">Resize on a new hardware cluster</span></span>
<span data-ttu-id="fc084-127">VM을 호스팅하는 하드웨어 클러스터에서 사용할 수 없는 크기로 VM을 크기 조정하려면 클라우드 서비스와 클라우드 서비스의 모든 VM을 다시 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-127">To resize a VM to a size not available in the hardware cluster hosting the VM, the cloud service and all VMs in the cloud service must be recreated.</span></span> <span data-ttu-id="fc084-128">각 클라우드 서비스는 단일 하드웨어 클러스터에서 호스트되므로 클라우드 서비스의 모든 VM은 하드웨어 클러스터에서 지원되는 크기여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-128">Each cloud service is hosted on a single hardware cluster so all VMs in the cloud service must be a size that is supported on a hardware cluster.</span></span> <span data-ttu-id="fc084-129">다음 단계에서는 클라우드 서비스를 삭제한 후 다시 만들어 VM 크기를 조정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-129">The following steps will describe how to resize a VM by deleting and then recreating the cloud service.</span></span>

1. <span data-ttu-id="fc084-130">지역에서 사용할 수 있는 VM 크기를 나열하려면 다음 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-130">Run the following PowerShell command to list the VM sizes available in the region.</span></span> 
   
    ```powershell
    Get-AzureLocation | where {$_.Name -eq "<locationName>"}
    ```
2. <span data-ttu-id="fc084-131">크기 조정할 VM을 포함하는 클라우드 서비스의 각 VM에 대한 모든 구성 설정을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-131">Make note of all configuration settings for each VM in the cloud service which contains the VM to be resized.</span></span> 
3. <span data-ttu-id="fc084-132">각 VM에 대한 디스크를 유지하는 옵션을 선택하는 클라우드 서비스에서 모든 VM을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-132">Delete all VMs in the cloud service selecting the option to retain the disks for each VM.</span></span>
4. <span data-ttu-id="fc084-133">원하는 VM 크기를 사용하여 크기를 조정하도록 VM을 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-133">Recreate the VM to be resized using the desired VM size.</span></span>
5. <span data-ttu-id="fc084-134">이제 클라우드 서비스를 호스팅하는 하드웨어 클러스터에서 사용할 수 있는 VM 크기를 사용하여 클라우드 서비스에 있는 다른 모든 VM을 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-134">Recreate all other VMs which were in the cloud service using a VM size available in the hardware cluster now hosting the cloud service.</span></span>

<span data-ttu-id="fc084-135">새 VM 크기를 사용하여 클라우드 서비스를 삭제하고 다시 만드는 샘플 스크립트는 [여기](https://github.com/Azure/azure-vm-scripts)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc084-135">A sample script for deleting and recreating a cloud service using a new VM size can be found [here](https://github.com/Azure/azure-vm-scripts).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="fc084-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fc084-136">Next steps</span></span>
* <span data-ttu-id="fc084-137">[Resource Manager 배포 모델에서 만든 VM 크기 조정](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fc084-137">[Resize a VM created in the Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

