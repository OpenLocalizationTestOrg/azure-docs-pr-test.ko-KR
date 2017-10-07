---
title: "Azure CLI 1.0 hello로 Linux VM의 복사본을 aaaCreate | Microsoft Docs"
description: "와 Azure Linux 가상 컴퓨터의 복사본 toocreate Azure CLI 1.0 hello 리소스 관리자 배포 모델에서 hello 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: 997a2c8109e7083ececd76fd1013e9ed4d3e6afd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-hello-azure-cli-10"></a><span data-ttu-id="602da-103">Azure CLI 1.0 hello로 Azure에서 실행 중인 Linux 가상 컴퓨터의 복사본 만들기</span><span class="sxs-lookup"><span data-stu-id="602da-103">Create a copy of a Linux virtual machine running on Azure with hello Azure CLI 1.0</span></span>
<span data-ttu-id="602da-104">이 문서에서는 toocreate Azure 가상 컴퓨터 (VM) 실행 중인 Linux 사용 하 여 프로그램의 복사본을 리소스 관리자 배포 모델을 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="602da-104">This article shows you how toocreate a copy of your Azure virtual machine (VM) running Linux using hello Resource Manager deployment model.</span></span> <span data-ttu-id="602da-105">먼저 hello 운영 체제 및 데이터 디스크 tooa 새 컨테이너를 통해 다음 hello 네트워크 리소스를 설정 복사한 hello 새 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="602da-105">First you copy over hello operating system and data disks tooa new container, then set up hello network resources and create hello new virtual machine.</span></span>

<span data-ttu-id="602da-106">[사용자 지정 디스크 이미지에서 VM 업로드 및 만들](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602da-106">You can also [upload and create a VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="602da-107">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="602da-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="602da-108">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602da-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="602da-109">Azure CLI 1.0 – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)</span><span class="sxs-lookup"><span data-stu-id="602da-109">Azure CLI 1.0 – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="602da-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한</span><span class="sxs-lookup"><span data-stu-id="602da-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="602da-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="602da-111">Before you begin</span></span>
<span data-ttu-id="602da-112">Hello hello 단계를 시작 하기 전에 필수 구성 요소를 다음을 충족 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="602da-112">Ensure that you meet hello following prerequisites before you start hello steps:</span></span>

* <span data-ttu-id="602da-113">Hello 있는 [Azure CLI](../../cli-install-nodejs.md) 다운로드 하 고 컴퓨터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="602da-113">You have hello [Azure CLI](../../cli-install-nodejs.md) downloaded and installed on your machine.</span></span> 
* <span data-ttu-id="602da-114">또한 기존 Azure Linux VM에 대한 다음과 같은 몇 가지 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="602da-114">You also need some information about your existing Azure Linux VM:</span></span>

| <span data-ttu-id="602da-115">소스 VM 정보</span><span class="sxs-lookup"><span data-stu-id="602da-115">Source VM information</span></span> | <span data-ttu-id="602da-116">여기서 tooget 것</span><span class="sxs-lookup"><span data-stu-id="602da-116">Where tooget it</span></span> |
| --- | --- |
| <span data-ttu-id="602da-117">VM 이름</span><span class="sxs-lookup"><span data-stu-id="602da-117">VM name</span></span> |`azure vm list` |
| <span data-ttu-id="602da-118">리소스 그룹 이름</span><span class="sxs-lookup"><span data-stu-id="602da-118">Resource Group name</span></span> |`azure vm list` |
| <span data-ttu-id="602da-119">위치</span><span class="sxs-lookup"><span data-stu-id="602da-119">Location</span></span> |`azure vm list` |
| <span data-ttu-id="602da-120">저장소 계정 이름</span><span class="sxs-lookup"><span data-stu-id="602da-120">Storage Account name</span></span> |`azure storage account list -g <resourceGroup>` |
| <span data-ttu-id="602da-121">컨테이너 이름</span><span class="sxs-lookup"><span data-stu-id="602da-121">Container name</span></span> |`azure storage container list -a <sourcestorageaccountname>` |
| <span data-ttu-id="602da-122">소스 VM VHD 파일 이름</span><span class="sxs-lookup"><span data-stu-id="602da-122">Source VM VHD file name</span></span> |`azure storage blob list --container <containerName>` |

* <span data-ttu-id="602da-123">새 VM에 대 한 약간의 조정이 toomake이 필요 합니다.   </span><span class="sxs-lookup"><span data-stu-id="602da-123">You will need toomake some choices about your new VM:    </span></span><br> <span data-ttu-id="602da-124">-컨테이너 이름    </span><span class="sxs-lookup"><span data-stu-id="602da-124">-Container name    </span></span><br> <span data-ttu-id="602da-125">-VM 이름    </span><span class="sxs-lookup"><span data-stu-id="602da-125">-VM name    </span></span><br> <span data-ttu-id="602da-126">-VM 크기    </span><span class="sxs-lookup"><span data-stu-id="602da-126">-VM size    </span></span><br> <span data-ttu-id="602da-127">-vNet 이름    </span><span class="sxs-lookup"><span data-stu-id="602da-127">-vNet name    </span></span><br> <span data-ttu-id="602da-128">-SubNet 이름    </span><span class="sxs-lookup"><span data-stu-id="602da-128">-SubNet name    </span></span><br> <span data-ttu-id="602da-129">-IP 이름    </span><span class="sxs-lookup"><span data-stu-id="602da-129">-IP Name    </span></span><br> <span data-ttu-id="602da-130">-NIC 이름</span><span class="sxs-lookup"><span data-stu-id="602da-130">-NIC name</span></span>

## <a name="login-and-set-your-subscription"></a><span data-ttu-id="602da-131">로그인 및 구독 설정</span><span class="sxs-lookup"><span data-stu-id="602da-131">Login and set your subscription</span></span>
1. <span data-ttu-id="602da-132">로그인 toohello CLI 합니다.</span><span class="sxs-lookup"><span data-stu-id="602da-132">Login toohello CLI.</span></span>

    ```azurecli
    azure login
    ```
2. <span data-ttu-id="602da-133">Resource Manager 모드에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="602da-133">Make sure you are in Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="602da-134">Hello 올바른 구독을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="602da-134">Set hello correct subscription.</span></span> <span data-ttu-id="602da-135">'Azure 계정 목록' toosee에서는 모든 구독.</span><span class="sxs-lookup"><span data-stu-id="602da-135">You can use 'azure account list' toosee all of your subscriptions.</span></span>

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-hello-vm"></a><span data-ttu-id="602da-136">Hello VM 중지</span><span class="sxs-lookup"><span data-stu-id="602da-136">Stop hello VM</span></span>
<span data-ttu-id="602da-137">중지 하 고 hello 원본 VM 할당을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="602da-137">Stop and deallocate hello source VM.</span></span> <span data-ttu-id="602da-138">구독 및 해당 리소스 그룹 이름은 'azure vm 목록' tooget hello Vm의 모든 목록을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602da-138">You can use 'azure vm list' tooget a list of all of hello VMs in your subscription and their resource group names.</span></span>

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-hello-vhd"></a><span data-ttu-id="602da-139">Hello VHD 복사</span><span class="sxs-lookup"><span data-stu-id="602da-139">Copy hello VHD</span></span>
<span data-ttu-id="602da-140">Hello를 사용 하 여 hello 원본 저장소 toohello 대상에서 hello VHD를 복사할 수 있습니다 `azure storage blob copy start`합니다.</span><span class="sxs-lookup"><span data-stu-id="602da-140">You can copy hello VHD from hello source storage toohello destination using hello `azure storage blob copy start`.</span></span> <span data-ttu-id="602da-141">이 예제에서는 toocopy hello VHD toohello 것 이며 동일한 저장소 계정에는 있지만 다른 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="602da-141">In this example, we are going toocopy hello VHD toohello same storage account, but a different container.</span></span>

<span data-ttu-id="602da-142">toocopy hello VHD tooanother 컨테이너 hello에 동일한 저장소 계정, 유형:</span><span class="sxs-lookup"><span data-stu-id="602da-142">toocopy hello VHD tooanother container in hello same storage account, type:</span></span>

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-hello-virtual-network-for-your-new-vm"></a><span data-ttu-id="602da-143">새 VM에 대 한 hello 가상 네트워크를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="602da-143">Set up hello virtual network for your new VM</span></span>
<span data-ttu-id="602da-144">새 VM에 대한 가상 네트워크 및 NIC를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="602da-144">Set up a virtual network and NIC for your new VM.</span></span> 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-hello-new-vm"></a><span data-ttu-id="602da-145">만들 새 VM hello</span><span class="sxs-lookup"><span data-stu-id="602da-145">Create hello new VM</span></span>
<span data-ttu-id="602da-146">업로드 된 가상 디스크에서 이제 VM을 만들 수 있습니다 [리소스 관리자 템플릿을 사용 하 여](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) 또는 디스크를 입력 하 여 hello URI tooyour를 지정 하 여 CLI hello를 통해 복사:</span><span class="sxs-lookup"><span data-stu-id="602da-146">You can now create a VM from your uploaded virtual disk [using a resource manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) or through hello CLI by specifying hello URI tooyour copied disk by typing:</span></span>

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a><span data-ttu-id="602da-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="602da-147">Next steps</span></span>
<span data-ttu-id="602da-148">toolearn 어떻게 toouse Azure CLI toomanage 새 가상 컴퓨터에 참조 [hello Azure 리소스 관리자에 대 한 Azure CLI 명령을](../azure-cli-arm-commands.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="602da-148">toolearn how toouse Azure CLI toomanage your new virtual machine, see [Azure CLI commands for hello Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>

