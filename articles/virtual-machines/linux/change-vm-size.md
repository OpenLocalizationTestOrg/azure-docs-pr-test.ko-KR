---
title: "aaaHow tooresize hello Azure CLI 2.0을 사용 하 여 Linux VM | Microsoft Docs"
description: "어떻게를 tooscale 또는 비율을 변경 하 여 Linux 가상 컴퓨터를 hello VM 크기입니다."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: e163f878-b919-45c5-9f5a-75a64f3b14a0
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2017
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e8fba485b5bcc7824f546de5cf3df77624a28008
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a><span data-ttu-id="2c0cb-103">CLI 2.0을 사용하여 Linux 가상 컴퓨터 크기 조정</span><span class="sxs-lookup"><span data-stu-id="2c0cb-103">Resize a Linux virtual machine using CLI 2.0</span></span>

<span data-ttu-id="2c0cb-104">가상 컴퓨터 (VM)를 프로 비전 한 후 확장할 수 있습니다 hello VM 위로 또는 아래로 hello를 변경 하 여 [VM 크기][vm-sizes]합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-104">After you provision a virtual machine (VM), you can scale hello VM up or down by changing hello [VM size][vm-sizes].</span></span> <span data-ttu-id="2c0cb-105">경우에 따라 할당을 취소 해야 hello VM 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-105">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="2c0cb-106">Hello hello VM을 호스팅하는 hello 하드웨어 클러스터에 사용할 수 없는 크기 원하는 toodeallocate hello VM 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-106">You need toodeallocate hello VM if hello desired size is not available on hello hardware cluster that is hosting hello VM.</span></span> <span data-ttu-id="2c0cb-107">이 문서를 사용 하 여 Linux VM tooresize Azure CLI 2.0 hello 하는 방법을 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-107">This article details how tooresize a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="2c0cb-108">Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-108">You can also perform these steps with hello [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="resize-a-vm"></a><span data-ttu-id="2c0cb-109">VM 크기 조정</span><span class="sxs-lookup"><span data-stu-id="2c0cb-109">Resize a VM</span></span>
<span data-ttu-id="2c0cb-110">VM tooresize 필요한 hello 최신 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 사용 하 여 Azure 계정 tooan [az 로그인](/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-110">tooresize a VM, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

1. <span data-ttu-id="2c0cb-111">Hello 하드웨어 클러스터 VM hello로 호스트 되는 위치에서 사용 가능한 VM hello 목록 보기의 크기를 조정 [az vm 목록-vm-크기 조정-옵션](/cli/azure/vm#list-vm-resize-options)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-111">View hello list of available VM sizes on hello hardware cluster where hello VM is hosted with [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span></span> <span data-ttu-id="2c0cb-112">hello 다음 예에서는 나열 hello 라는 VM에 대 한 VM 크기 `myVM` hello 리소스 그룹에 `myResourceGroup` 영역:</span><span class="sxs-lookup"><span data-stu-id="2c0cb-112">hello following example lists VM sizes for hello VM named `myVM` in hello resource group `myResourceGroup` region:</span></span>
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. <span data-ttu-id="2c0cb-113">VM 크기 나열 된 hello 필요한 경우 크기 조정의 VM hello [az vm 크기를 조정](/cli/azure/vm#resize)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-113">If hello desired VM size is listed, resize hello VM with [az vm resize](/cli/azure/vm#resize).</span></span> <span data-ttu-id="2c0cb-114">다음 예제에서는 크기가 조정 되어 hello hello 라는 VM `myVM` toohello `Standard_DS3_v2` 크기:</span><span class="sxs-lookup"><span data-stu-id="2c0cb-114">hello following example resizes hello VM named `myVM` toohello `Standard_DS3_v2` size:</span></span>
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    <span data-ttu-id="2c0cb-115">이 프로세스 동안 hello VM 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-115">hello VM restarts during this process.</span></span> <span data-ttu-id="2c0cb-116">Hello 다시 시작한 후 기존 OS 및 데이터 디스크는 다시 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-116">After hello restart, your existing OS and data disks are remapped.</span></span> <span data-ttu-id="2c0cb-117">Hello 임시 디스크에 있는 모든 내용을 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-117">Anything on hello temporary disk is lost.</span></span>

3. <span data-ttu-id="2c0cb-118">Toofirst hello VM 크기 나열 되지 않으면 원하는 경우 해야 할당을 취소의 VM hello [az vm 할당을 취소](/cli/azure/vm#deallocate)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-118">If hello desired VM size is not listed, you need toofirst deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="2c0cb-119">이 프로세스 영역에서는 hello 및 후에 시작 하는 크기가 조정 된 tooany 크기로 사용할 수 있는 hello VM toothen을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-119">This process allows hello VM toothen be resized tooany size available that hello region supports and then started.</span></span> <span data-ttu-id="2c0cb-120">hello 다음 단계 할당 해제, 크기 조정 및 다음 hello 라는 VM을 시작 `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="2c0cb-120">hello following steps deallocate, resize, and then start hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="2c0cb-121">또한 할당 해제 hello VM toohello VM을 할당 하는 동적 IP 주소를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-121">Deallocating hello VM also releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="2c0cb-122">hello OS 및 데이터 디스크 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-122">hello OS and data disks are not affected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c0cb-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2c0cb-123">Next steps</span></span>
<span data-ttu-id="2c0cb-124">확장성을 높이기 위해서는 여러 VM 인스턴스를 실행하고 규모를 확장합니다. 자세한 내용은 [가상 컴퓨터 확장 집합에서 Linux 컴퓨터 자동 확장][scale-set]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-124">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
