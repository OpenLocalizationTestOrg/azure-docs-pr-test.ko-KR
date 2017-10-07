---
title: "Azure에서 Linux 가상 컴퓨터 aaaRedeploy | Microsoft Docs"
description: "어떻게 tooredeploy Linux 가상 컴퓨터에서 Azure toomitigate SSH 연결을 발급 합니다."
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
ms.openlocfilehash: 9adfd1b11f262d362133366b2bba5e69c70c9b82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-linux-virtual-machine-toonew-azure-node"></a><span data-ttu-id="5e732-103">Linux 가상 컴퓨터 toonew Azure 노드를 다시 배포</span><span class="sxs-lookup"><span data-stu-id="5e732-103">Redeploy Linux virtual machine toonew Azure node</span></span>
<span data-ttu-id="5e732-104">SSH 문제를 해결 하는 때 어려움을 겪을 또는 응용 프로그램이 Azure에서 tooa Linux 가상 컴퓨터 (VM)를 액세스, hello VM을 다시 배포 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e732-104">If you face difficulties troubleshooting SSH or application access tooa Linux virtual machine (VM) in Azure, redeploying hello VM may help.</span></span> <span data-ttu-id="5e732-105">VM을 다시 배포할 때 hello VM tooa hello Azure 인프라 내에서 새 노드를 이동 하 고 다시 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e732-105">When you redeploy a VM, it moves hello VM tooa new node within hello Azure infrastructure and then powers it back on.</span></span> <span data-ttu-id="5e732-106">모든 구성 옵션 및 관련 리소스는 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e732-106">All your configuration options and associated resources are retained.</span></span> <span data-ttu-id="5e732-107">이 문서에서는 Azure CLI 또는 hello Azure 포털을 사용 하 여 VM a tooredeploy 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e732-107">This article shows you how tooredeploy a VM using Azure CLI or hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="5e732-108">VM을 다시 배포 후에 hello 임시 디스크 손실 되 고 가상 네트워크 인터페이스와 연결 된 동적 IP 주소는 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e732-108">After you redeploy a VM, hello temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 

<span data-ttu-id="5e732-109">Hello 다음 옵션 중 하나를 사용 하는 VM을 다시 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e732-109">You can redeploy a VM using one of hello following options.</span></span> <span data-ttu-id="5e732-110">하나의 옵션 tooredeploy toochoose VM만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5e732-110">You only need toochoose one option tooredeploy your VM:</span></span>

- [<span data-ttu-id="5e732-111">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5e732-111">Azure CLI 2.0</span></span>](#azure-cli-20)
- [<span data-ttu-id="5e732-112">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5e732-112">Azure CLI 1.0</span></span>](#azure-cli-10)
- [<span data-ttu-id="5e732-113">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="5e732-113">Azure portal</span></span>](#using-azure-portal)

## <a name="use-hello-azure-cli-20"></a><span data-ttu-id="5e732-114">Hello Azure CLI 2.0을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="5e732-114">Use hello Azure CLI 2.0</span></span>
<span data-ttu-id="5e732-115">최신 설치 hello [Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 계정을 사용 하 여 로그인 [az 로그인](/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e732-115">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="5e732-116">[az vm redeploy](/cli/azure/vm#redeploy)를 사용하여 VM을 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="5e732-116">Redeploy your VM with [az vm redeploy](/cli/azure/vm#redeploy).</span></span> <span data-ttu-id="5e732-117">다음 예에서는 재배포 시 hello hello 라는 VM *myVM* 이라는 hello 리소스 그룹에 *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="5e732-117">hello following example redeploys hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-hello-azure-cli-10"></a><span data-ttu-id="5e732-118">Hello Azure CLI 1.0을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="5e732-118">Use hello Azure CLI 1.0</span></span>
<span data-ttu-id="5e732-119">Hello 설치 [최신 Azure CLI 1.0](../../cli-install-nodejs.md)tooan Azure 계정에에서 로그인 하 고 리소스 관리자 모드에 있는지 확인 (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="5e732-119">Install hello [latest Azure CLI 1.0](../../cli-install-nodejs.md), log in tooan Azure account, and make sure that you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="5e732-120">다음 예에서는 재배포 시 hello hello 라는 VM *myVM* 이라는 hello 리소스 그룹에 *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="5e732-120">hello following example redeploys hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="5e732-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5e732-121">Next steps</span></span>
<span data-ttu-id="5e732-122">Tooyour VM을 연결 하는 데 문제가 있는 경우에 특별 한 도움말을 찾을 수 있습니다 [SSH 연결 문제 해결](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 [SSH 문제 해결 단계를 자세히](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e732-122">If you are having issues connecting tooyour VM, you can find specific help on [troubleshooting SSH connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [detailed SSH troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="5e732-123">VM에서 실행 중인 응용 프로그램에 액세스할 수 없는 경우 [응용 프로그램 문제 해결](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 읽어볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e732-123">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

