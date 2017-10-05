---
title: "Azure에서 Linux 가상 컴퓨터 다시 배포 | Microsoft Docs"
description: "Azure에서 가상 컴퓨터를 다시 배포하여 SSH 연결 문제를 완화하는 방법"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: e9530dd6-f5b0-4160-b36b-d75151d99eb7
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 7a8653a82775e718c38f65f246d997ba61f99d58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="redeploy-linux-virtual-machine-to-new-azure-node"></a><span data-ttu-id="a29c9-103">새 Azure 노드로 Linux 가상 컴퓨터 다시 배포</span><span class="sxs-lookup"><span data-stu-id="a29c9-103">Redeploy Linux virtual machine to new Azure node</span></span>
<span data-ttu-id="a29c9-104">Azure에서 Linux VM(가상 컴퓨터)에 대한 SSH 또는 응용 프로그램 액세스 문제를 해결하는 데 어려움이 있는 경우 VM을 다시 배포하는 것이 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a29c9-104">If you face difficulties troubleshooting SSH or application access to a Linux virtual machine (VM) in Azure, redeploying the VM may help.</span></span> <span data-ttu-id="a29c9-105">VM을 다시 배포하면 VM이 Azure 인프라 내의 새 노드로 이동된 다음 전원이 다시 켜집니다.</span><span class="sxs-lookup"><span data-stu-id="a29c9-105">When you redeploy a VM, it moves the VM to a new node within the Azure infrastructure and then powers it back on.</span></span> <span data-ttu-id="a29c9-106">모든 구성 옵션 및 관련 리소스는 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="a29c9-106">All your configuration options and associated resources are retained.</span></span> <span data-ttu-id="a29c9-107">이 문서에서는 Azure CLI 또는 Azure 포털을 사용하여 VM을 다시 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a29c9-107">This article shows you how to redeploy a VM using Azure CLI or the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="a29c9-108">VM을 다시 배포한 후에 임시 디스크가 손실되고 가상 네트워크 인터페이스와 연결된 동적 IP 주소가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="a29c9-108">After you redeploy a VM, the temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 

<span data-ttu-id="a29c9-109">다음 옵션 중 하나를 사용하여 VM을 다시 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a29c9-109">You can redeploy a VM using one of the following options.</span></span> <span data-ttu-id="a29c9-110">VM을 다시 배포하려면 하나의 옵션만을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29c9-110">You only need to choose one option to redeploy your VM:</span></span>

- [<span data-ttu-id="a29c9-111">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a29c9-111">Azure CLI 2.0</span></span>](#azure-cli-20)
- [<span data-ttu-id="a29c9-112">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a29c9-112">Azure CLI 1.0</span></span>](#azure-cli-10)
- [<span data-ttu-id="a29c9-113">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="a29c9-113">Azure portal</span></span>](#using-azure-portal)

## <a name="use-the-azure-cli-20"></a><span data-ttu-id="a29c9-114">Azure CLI 2.0 사용</span><span class="sxs-lookup"><span data-stu-id="a29c9-114">Use the Azure CLI 2.0</span></span>
<span data-ttu-id="a29c9-115">최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치하고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a29c9-115">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="a29c9-116">[az vm redeploy](/cli/azure/vm#redeploy)를 사용하여 VM을 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="a29c9-116">Redeploy your VM with [az vm redeploy](/cli/azure/vm#redeploy).</span></span> <span data-ttu-id="a29c9-117">다음 예제에서는 리소스 그룹 *myResourceGroup*에서 *myVM*이라는 VM을 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="a29c9-117">The following example redeploys the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-the-azure-cli-10"></a><span data-ttu-id="a29c9-118">Azure CLI 1.0 사용</span><span class="sxs-lookup"><span data-stu-id="a29c9-118">Use the Azure CLI 1.0</span></span>
<span data-ttu-id="a29c9-119">[최신 Azure CLI 1.0](../../cli-install-nodejs.md)을 설치하고 Azure 계정에 로그인하고 리소스 관리자 모드에 있는지 확인합니다(`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="a29c9-119">Install the [latest Azure CLI 1.0](../../cli-install-nodejs.md), log in to an Azure account, and make sure that you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="a29c9-120">다음 예제에서는 리소스 그룹 *myResourceGroup*에서 *myVM*이라는 VM을 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="a29c9-120">The following example redeploys the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="a29c9-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a29c9-121">Next steps</span></span>
<span data-ttu-id="a29c9-122">VM에 연결하는 데 문제가 있는 경우 [SSH 연결 문제 해결](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 [자세한 SSH 문제 해결 단계](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 특정 도움말을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a29c9-122">If you are having issues connecting to your VM, you can find specific help on [troubleshooting SSH connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [detailed SSH troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="a29c9-123">VM에서 실행 중인 응용 프로그램에 액세스할 수 없는 경우 [응용 프로그램 문제 해결](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 읽어볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a29c9-123">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

