---
title: "Azure에서 Linux VM 템플릿에서 aaaCreate | Microsoft Docs"
description: "어떻게 toouse hello Azure CLI 2.0 toocreate 리소스 관리자 템플릿으로 Linux VM"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f4b8c4103cccbae13c679ff2a2cac928a0e8e809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-with-azure-resource-manager-templates"></a><span data-ttu-id="e388d-103">어떻게 toocreate Azure 리소스 관리자 템플릿으로 Linux 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="e388d-103">How toocreate a Linux virtual machine with Azure Resource Manager templates</span></span>
<span data-ttu-id="e388d-104">이 문서에서는 tooquickly hello Azure CLI 2.0 및 Azure 리소스 관리자 템플릿을 사용 하 여 Linux 가상 컴퓨터 (VM)를 배포 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e388d-104">This article shows you how tooquickly deploy a Linux virtual machine (VM) with Azure Resource Manager templates and hello Azure CLI 2.0.</span></span> <span data-ttu-id="e388d-105">Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e388d-105">You can also perform these steps with hello [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span></span>


## <a name="templates-overview"></a><span data-ttu-id="e388d-106">템플릿 개요</span><span class="sxs-lookup"><span data-stu-id="e388d-106">Templates overview</span></span>
<span data-ttu-id="e388d-107">Azure 리소스 관리자 템플릿은 hello 인프라 및 Azure 솔루션의 구성을 정의 하는 JSON 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e388d-107">Azure Resource Manager templates are JSON files that define hello infrastructure and configuration of your Azure solution.</span></span> <span data-ttu-id="e388d-108">템플릿을 사용하여 수명 주기 내내 솔루션을 반복적으로 배포하고 안심하고 일관된 상태로 리소스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e388d-108">By using a template, you can repeatedly deploy your solution throughout its lifecycle and have confidence your resources are deployed in a consistent state.</span></span> <span data-ttu-id="e388d-109">hello 형식의 hello 템플릿과 작성 하는 방법에 대해 자세히 toolearn 참조 [첫 번째 Azure 리소스 관리자 서식 파일 만들기](../../azure-resource-manager/resource-manager-create-first-template.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e388d-109">toolearn more about hello format of hello template and how you construct it, see [Create your first Azure Resource Manager template](../../azure-resource-manager/resource-manager-create-first-template.md).</span></span> <span data-ttu-id="e388d-110">tooview hello 리소스 형식에 대 한 JSON 구문을 참조 [Azure 리소스 관리자 템플릿을에 리소스를 정의](/azure/templates/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e388d-110">tooview hello JSON syntax for resources types, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span>


## <a name="create-resource-group"></a><span data-ttu-id="e388d-111">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="e388d-111">Create resource group</span></span>
<span data-ttu-id="e388d-112">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="e388d-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="e388d-113">가상 컴퓨터보다 먼저 리소스 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e388d-113">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="e388d-114">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroupVM* hello에 *eastus* 영역:</span><span class="sxs-lookup"><span data-stu-id="e388d-114">hello following example creates a resource group named *myResourceGroupVM* in hello *eastus* region:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="e388d-115">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="e388d-115">Create virtual machine</span></span>
<span data-ttu-id="e388d-116">hello 다음 예제에서는에서 VM [이 Azure 리소스 관리자 템플릿을](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) 와 [az 그룹 배포 만들기](/cli/azure/group/deployment#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="e388d-116">hello following example creates a VM from [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="e388d-117">사용자 고유의 SSH 공개 키를 hello 내용의 등의 hello 값을 제공 *~/.ssh/id_rsa.pub*합니다.</span><span class="sxs-lookup"><span data-stu-id="e388d-117">Provide hello value of your own SSH public key, such as hello contents of *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="e388d-118">SSH 키 쌍 toocreate 필요한 경우 참조 [어떻게 toocreate 및 사용 된 SSH 키 쌍 Azure에서 Linux Vm에 대 한](mac-create-ssh-keys.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e388d-118">If you need toocreate an SSH key pair, see [How toocreate and use an SSH key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

<span data-ttu-id="e388d-119">이 예제에서는 GitHub에 저장된 템플릿을 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="e388d-119">In this example, you specified a template stored in GitHub.</span></span> <span data-ttu-id="e388d-120">있습니다 수 또한 다운로드 또는 템플릿을 만들고 hello로 hello 로컬 경로 지정 합니다. 동일한 `--template-file` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="e388d-120">You can also download or create a template and specify hello local path with hello same `--template-file` parameter.</span></span>

<span data-ttu-id="e388d-121">tooSSH tooyour VM을 hello와 공용 IP 주소를 가져올 [az 네트워크 공개 ip 표시](/cli/azure/network/public-ip#show):</span><span class="sxs-lookup"><span data-stu-id="e388d-121">tooSSH tooyour VM, obtain hello public IP address with [az network public-ip show](/cli/azure/network/public-ip#show):</span></span>

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="e388d-122">그런 다음 SSH tooyour VM 정상적으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e388d-122">You can then SSH tooyour VM as normal:</span></span>

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a><span data-ttu-id="e388d-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e388d-123">Next steps</span></span>
<span data-ttu-id="e388d-124">이 예제에서는 기본 Linux VM을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="e388d-124">In this example, you created a basic Linux VM.</span></span> <span data-ttu-id="e388d-125">응용 프로그램 프레임 워크를 포함 하거나 더 복잡 한 환경을 만들 수 있는 더 많은 리소스 관리자 템플릿에 대 한 찾아보기 hello [Azure 빠른 시작 템플릿 갤러리](https://azure.microsoft.com/documentation/templates/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e388d-125">For more Resource Manager templates that include application frameworks or create more complex environments, browse hello [Azure quickstart templates gallery](https://azure.microsoft.com/documentation/templates/).</span></span>
