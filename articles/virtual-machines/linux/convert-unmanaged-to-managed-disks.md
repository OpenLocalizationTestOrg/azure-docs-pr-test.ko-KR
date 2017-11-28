---
title: "Azure의 Linux 가상 컴퓨터를 비관리 디스크에서 Managed Disks로 변환 - Azure Managed Disks | Microsoft Docs"
description: "Resource Manager 배포 모델에서 Azure CLI 2.0을 사용하여 Linux VM을 비관리 디스크에서 Managed Disks로 변환하는 방법"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 94f8e3330fb2d6547811315fcfdb8ced338e0247
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-to-managed-disks"></a><span data-ttu-id="b8750-103">Linux 가상 컴퓨터를 비관리 디스크에서 Managed Disks로 변환</span><span class="sxs-lookup"><span data-stu-id="b8750-103">Convert a Linux virtual machine from unmanaged disks to managed disks</span></span>

<span data-ttu-id="b8750-104">비관리 디스크를 사용하는 기존 Linux VM(가상 컴퓨터)이 있는 경우 [Azure Managed Disks](../windows/managed-disks-overview.md) 서비스를 통해 Managed Disks를 사용하도록 VM을 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8750-104">If you have existing Linux virtual machines (VMs) that use unmanaged disks, you can convert the VMs to use managed disks through the [Azure Managed Disks](../windows/managed-disks-overview.md) service.</span></span> <span data-ttu-id="b8750-105">이 프로세스는 OS 디스크와 연결된 데이터 디스크를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="b8750-105">This process converts both the OS disk and any attached data disks.</span></span>

<span data-ttu-id="b8750-106">이 문서에서는 Azure CLI를 사용하여 VM을 변환하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b8750-106">This article shows you how to convert VMs by using the Azure CLI.</span></span> <span data-ttu-id="b8750-107">CLI를 설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치](/cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8750-107">If you need to install or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="b8750-108">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="b8750-108">Before you begin</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a><span data-ttu-id="b8750-109">단일 인스턴스 VM 변환</span><span class="sxs-lookup"><span data-stu-id="b8750-109">Convert single-instance VMs</span></span>
<span data-ttu-id="b8750-110">이 섹션에서는 단일 인스턴스 Azure VM을 비관리 디스크에서 Managed Disks로 변환하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b8750-110">This section covers how to convert single-instance Azure VMs from unmanaged disks to managed disks.</span></span> <span data-ttu-id="b8750-111">VM이 가용성 집합에 있는 경우 다음 섹션을 참조하세요. 이 프로세스를 사용하여 프리미엄(SSD) 비관리 디스크에서 프리미엄 Managed Disks로 또는 표준(HDD) 비관리 디스크에서 표준 Managed Disks로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8750-111">(If your VMs are in an availability set, see the next section.) You can use this process to convert the VMs from premium (SSD) unmanaged disks to premium managed disks, or from standard (HDD) unmanaged disks to standard managed disks.</span></span>

1. <span data-ttu-id="b8750-112">[az vm deallocate](/cli/azure/vm#deallocate)를 사용하여 VM의 할당을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="b8750-112">Deallocate the VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="b8750-113">다음 예제에서는 리소스 그룹 `myResourceGroup`에서 `myVM`이라는 VM의 할당을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="b8750-113">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. <span data-ttu-id="b8750-114">[az vm convert](/cli/azure/vm#convert)를 사용하여 VM을 Managed Disks로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="b8750-114">Convert the VM to managed disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="b8750-115">다음 프로세스는 OS 디스크 및 데이터 디스크를 포함하는 `myVM`이라는 VM을 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="b8750-115">The following process converts the VM named `myVM`, including the OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="b8750-116">[az vm start](/cli/azure/vm#start)를 사용하여 VM을 Managed Disks로 변환한 후 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b8750-116">Start the VM after the conversion to managed disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="b8750-117">다음 예제에서는 리소스 그룹 `myResourceGroup`의 VM `myVM`을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b8750-117">The following example starts the VM named `myVM` in the resource group named `myResourceGroup`.</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="b8750-118">가용성 집합의 VM 변환</span><span class="sxs-lookup"><span data-stu-id="b8750-118">Convert VMs in an availability set</span></span>

<span data-ttu-id="b8750-119">관리되는 디스크로 변환하려는 VM이 가용성 집합에 있는 경우 먼저 가용성 집합을 관리되는 가용성 집합으로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8750-119">If the VMs that you want to convert to managed disks are in an availability set, you first need to convert the availability set to a managed availability set.</span></span>

<span data-ttu-id="b8750-120">가용성 집합을 변환하기 전에 가용성 집합에 있는 모든 VM의 할당을 취소해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8750-120">All VMs in the availability set must be deallocated before you convert the availability set.</span></span> <span data-ttu-id="b8750-121">가용성 집합이 관리되는 가용성 집합으로 변환된 후 모든 VM을 관리되는 디스크로 변환하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8750-121">Plan to convert all VMs to managed disks after the availability set itself has been converted to a managed availability set.</span></span> <span data-ttu-id="b8750-122">그런 다음 모든 VM을 시작하고 정상적으로 운영을 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="b8750-122">Then, start all the VMs and continue operating as normal.</span></span>

1. <span data-ttu-id="b8750-123">[az vm availability-set list](/cli/azure/vm/availability-set#list)를 사용하여 가용성 집합의 모든 VM을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="b8750-123">List all VMs in an availability set by using [az vm availability-set list](/cli/azure/vm/availability-set#list).</span></span> <span data-ttu-id="b8750-124">다음 예제에서는 리소스 그룹 `myResourceGroup`의 가용성 집합 `myAvailabilitySet`에 있는 모든 VM을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="b8750-124">The following example lists all VMs in the availability set named `myAvailabilitySet` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. <span data-ttu-id="b8750-125">[az vm deallocate](/cli/azure/vm#deallocate)를 사용하여 모든 VM의 할당을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="b8750-125">Deallocate all the VMs by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="b8750-126">다음 예제에서는 리소스 그룹 `myResourceGroup`에서 `myVM`이라는 VM의 할당을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="b8750-126">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="b8750-127">[az vm availability-set convert](/cli/azure/vm/availability-set#convert)를 사용하여 가용성 집합을 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="b8750-127">Convert the availability set by using [az vm availability-set convert](/cli/azure/vm/availability-set#convert).</span></span> <span data-ttu-id="b8750-128">다음 예제에서는 리소스 그룹 `myResourceGroup`의 가용성 집합 `myAvailabilitySet`을 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="b8750-128">The following example converts the availability set named `myAvailabilitySet` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. <span data-ttu-id="b8750-129">[az vm convert](/cli/azure/vm#convert)를 사용하여 모든 VM을 Managed Disks로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="b8750-129">Convert all the VMs to managed disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="b8750-130">다음 프로세스는 OS 디스크 및 데이터 디스크를 포함하는 `myVM`이라는 VM을 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="b8750-130">The following process converts the VM named `myVM`, including the OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. <span data-ttu-id="b8750-131">[az vm start](/cli/azure/vm#start)를 사용하여 모든 VM을 Managed Disks로 변환한 후 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b8750-131">Start all the VMs after the conversion to managed disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="b8750-132">다음 예제에서는 리소스 그룹 `myResourceGroup`의 VM `myVM`을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b8750-132">The following example starts the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="b8750-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b8750-133">Next steps</span></span>
<span data-ttu-id="b8750-134">저장소 옵션에 대한 자세한 내용은 [Azure Managed Disks 개요](../windows/managed-disks-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8750-134">For more information about storage options, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>
