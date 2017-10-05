---
title: "Azure CLI 1.0을 사용하여 Linux VM의 복사본 만들기 | Microsoft Docs"
description: "Resource Manager 배포 모델에서 Azure CLI 1.0을 사용하여 Azure Linux 가상 컴퓨터의 복사본을 만드는 방법에 대해 알아보기"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 62ae54f3596c9383cbf3b401fcfdb42ecfdee63c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-the-azure-cli-10"></a><span data-ttu-id="7c2a2-103">Azure CLI 1.0을 사용하여 Azure에서 실행되는 Linux 가상 컴퓨터의 복사본 만들기</span><span class="sxs-lookup"><span data-stu-id="7c2a2-103">Create a copy of a Linux virtual machine running on Azure with the Azure CLI 1.0</span></span>
<span data-ttu-id="7c2a2-104">이 문서는 Resource Manager 배포 모델에서 Linux를 실행하는 Azure VM(가상 컴퓨터)의 복사본을 만드는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7c2a2-104">This article shows you how to create a copy of your Azure virtual machine (VM) running Linux using the Resource Manager deployment model.</span></span> <span data-ttu-id="7c2a2-105">먼저 운영 체제와 데이터 디스크를 새 컨테이너로 복사한 다음 네트워크 리소스를 설정하고 새 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c2a2-105">First you copy over the operating system and data disks to a new container, then set up the network resources and create the new virtual machine.</span></span>

<span data-ttu-id="7c2a2-106">[사용자 지정 디스크 이미지에서 VM 업로드 및 만들](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c2a2-106">You can also [upload and create a VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="7c2a2-107">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="7c2a2-107">CLI versions to complete the task</span></span>
<span data-ttu-id="7c2a2-108">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c2a2-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="7c2a2-109">Azure CLI 1.0 - 클래식 및 리소스 관리 배포 모델용 CLI(이 문서)</span><span class="sxs-lookup"><span data-stu-id="7c2a2-109">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="7c2a2-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - 리소스 관리 배포 모델용 차세대 CLI</span><span class="sxs-lookup"><span data-stu-id="7c2a2-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7c2a2-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="7c2a2-111">Before you begin</span></span>
<span data-ttu-id="7c2a2-112">다음 단계를 시작하기 전에 다음 필수 조건을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7c2a2-112">Ensure that you meet the following prerequisites before you start the steps:</span></span>

* <span data-ttu-id="7c2a2-113">컴퓨터에 [Azure CLI](../../cli-install-nodejs.md) 를 다운로드하여 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="7c2a2-113">You have the [Azure CLI](../../cli-install-nodejs.md) downloaded and installed on your machine.</span></span> 
* <span data-ttu-id="7c2a2-114">또한 기존 Azure Linux VM에 대한 다음과 같은 몇 가지 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7c2a2-114">You also need some information about your existing Azure Linux VM:</span></span>

| <span data-ttu-id="7c2a2-115">소스 VM 정보</span><span class="sxs-lookup"><span data-stu-id="7c2a2-115">Source VM information</span></span> | <span data-ttu-id="7c2a2-116">가져올 수 있는 위치</span><span class="sxs-lookup"><span data-stu-id="7c2a2-116">Where to get it</span></span> |
| --- | --- |
| <span data-ttu-id="7c2a2-117">VM 이름</span><span class="sxs-lookup"><span data-stu-id="7c2a2-117">VM name</span></span> |`azure vm list` |
| <span data-ttu-id="7c2a2-118">리소스 그룹 이름</span><span class="sxs-lookup"><span data-stu-id="7c2a2-118">Resource Group name</span></span> |`azure vm list` |
| <span data-ttu-id="7c2a2-119">위치</span><span class="sxs-lookup"><span data-stu-id="7c2a2-119">Location</span></span> |`azure vm list` |
| <span data-ttu-id="7c2a2-120">저장소 계정 이름</span><span class="sxs-lookup"><span data-stu-id="7c2a2-120">Storage Account name</span></span> |`azure storage account list -g <resourceGroup>` |
| <span data-ttu-id="7c2a2-121">컨테이너 이름</span><span class="sxs-lookup"><span data-stu-id="7c2a2-121">Container name</span></span> |`azure storage container list -a <sourcestorageaccountname>` |
| <span data-ttu-id="7c2a2-122">소스 VM VHD 파일 이름</span><span class="sxs-lookup"><span data-stu-id="7c2a2-122">Source VM VHD file name</span></span> |`azure storage blob list --container <containerName>` |

* <span data-ttu-id="7c2a2-123">새 VM에 대한 몇 가지 항목을 선택해야 합니다.    </span><span class="sxs-lookup"><span data-stu-id="7c2a2-123">You will need to make some choices about your new VM:    </span></span><br> <span data-ttu-id="7c2a2-124">-컨테이너 이름    </span><span class="sxs-lookup"><span data-stu-id="7c2a2-124">-Container name    </span></span><br> <span data-ttu-id="7c2a2-125">-VM 이름    </span><span class="sxs-lookup"><span data-stu-id="7c2a2-125">-VM name    </span></span><br> <span data-ttu-id="7c2a2-126">-VM 크기    </span><span class="sxs-lookup"><span data-stu-id="7c2a2-126">-VM size    </span></span><br> <span data-ttu-id="7c2a2-127">-vNet 이름    </span><span class="sxs-lookup"><span data-stu-id="7c2a2-127">-vNet name    </span></span><br> <span data-ttu-id="7c2a2-128">-SubNet 이름    </span><span class="sxs-lookup"><span data-stu-id="7c2a2-128">-SubNet name    </span></span><br> <span data-ttu-id="7c2a2-129">-IP 이름    </span><span class="sxs-lookup"><span data-stu-id="7c2a2-129">-IP Name    </span></span><br> <span data-ttu-id="7c2a2-130">-NIC 이름</span><span class="sxs-lookup"><span data-stu-id="7c2a2-130">-NIC name</span></span>

## <a name="login-and-set-your-subscription"></a><span data-ttu-id="7c2a2-131">로그인 및 구독 설정</span><span class="sxs-lookup"><span data-stu-id="7c2a2-131">Login and set your subscription</span></span>
1. <span data-ttu-id="7c2a2-132">CLI에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7c2a2-132">Login to the CLI.</span></span>

    ```azurecli
    azure login
    ```
2. <span data-ttu-id="7c2a2-133">Resource Manager 모드에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7c2a2-133">Make sure you are in Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="7c2a2-134">올바른 구독을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c2a2-134">Set the correct subscription.</span></span> <span data-ttu-id="7c2a2-135">'azure account list'를 사용하여 모든 구독을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c2a2-135">You can use 'azure account list' to see all of your subscriptions.</span></span>

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-the-vm"></a><span data-ttu-id="7c2a2-136">VM을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="7c2a2-136">Stop the VM</span></span>
<span data-ttu-id="7c2a2-137">중지하고 소스 VM 할당을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="7c2a2-137">Stop and deallocate the source VM.</span></span> <span data-ttu-id="7c2a2-138">'azure vm list'를 사용하여 구독의 모든 VM 목록과 해당 리소스 그룹 이름을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c2a2-138">You can use 'azure vm list' to get a list of all of the VMs in your subscription and their resource group names.</span></span>

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-the-vhd"></a><span data-ttu-id="7c2a2-139">VHD 복사</span><span class="sxs-lookup"><span data-stu-id="7c2a2-139">Copy the VHD</span></span>
<span data-ttu-id="7c2a2-140">`azure storage blob copy start`사용하여 소스 저장소에서 대상으로 VHD를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c2a2-140">You can copy the VHD from the source storage to the destination using the `azure storage blob copy start`.</span></span> <span data-ttu-id="7c2a2-141">이 예제에서는 VHD를 동일한 저장소 계정의 다른 컨테이너에 VHD를 복사하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c2a2-141">In this example, we are going to copy the VHD to the same storage account, but a different container.</span></span>

<span data-ttu-id="7c2a2-142">동일한 저장소 계정의 다른 컨테이너에 VHD를 복사하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7c2a2-142">To copy the VHD to another container in the same storage account, type:</span></span>

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-the-virtual-network-for-your-new-vm"></a><span data-ttu-id="7c2a2-143">새 VM에 대한 가상 네트워크 설정</span><span class="sxs-lookup"><span data-stu-id="7c2a2-143">Set up the virtual network for your new VM</span></span>
<span data-ttu-id="7c2a2-144">새 VM에 대한 가상 네트워크 및 NIC를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c2a2-144">Set up a virtual network and NIC for your new VM.</span></span> 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-the-new-vm"></a><span data-ttu-id="7c2a2-145">새 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="7c2a2-145">Create the new VM</span></span>
<span data-ttu-id="7c2a2-146">이제 [Resource Manager 템플릿을 사용하거나](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) 다음을 입력하여 복사한 디스크에 대한 URI을 지정하는 방식으로 CLI를 통해 업로드된 가상 디스크에서 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c2a2-146">You can now create a VM from your uploaded virtual disk [using a resource manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) or through the CLI by specifying the URI to your copied disk by typing:</span></span>

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a><span data-ttu-id="7c2a2-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7c2a2-147">Next steps</span></span>
<span data-ttu-id="7c2a2-148">Azure CLI를 사용하여 새 가상 컴퓨터를 관리하는 방법을 알아보려면 [Azure Resource Manager의 Azure CLI 명령](../azure-cli-arm-commands.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c2a2-148">To learn how to use Azure CLI to manage your new virtual machine, see [Azure CLI commands for the Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>

