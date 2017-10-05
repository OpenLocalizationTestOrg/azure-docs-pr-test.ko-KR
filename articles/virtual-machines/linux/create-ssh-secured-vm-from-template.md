---
title: "템플릿에서 Azure에 Linux VM 만들기 | Microsoft Docs"
description: "Azure CLI 2.0을 사용하여 Resource Manager 템플릿에서 Linux VM을 만드는 방법"
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
ms.openlocfilehash: 908a8a0c82b2d21fb25c9b33dbd714570d1ac272
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-linux-virtual-machine-with-azure-resource-manager-templates"></a><span data-ttu-id="09ab1-103">Azure Resource Manager 템플릿을 사용하여 Linux 가상 컴퓨터를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="09ab1-103">How to create a Linux virtual machine with Azure Resource Manager templates</span></span>
<span data-ttu-id="09ab1-104">이 문서에서는 Azure Resource Manager 템플릿 및 Azure CLI 2.0을 사용하여 Linux VM(가상 컴퓨터)을 신속하게 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="09ab1-104">This article shows you how to quickly deploy a Linux virtual machine (VM) with Azure Resource Manager templates and the Azure CLI 2.0.</span></span> <span data-ttu-id="09ab1-105">[Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md)에서 이러한 단계를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09ab1-105">You can also perform these steps with the [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span></span>


## <a name="templates-overview"></a><span data-ttu-id="09ab1-106">템플릿 개요</span><span class="sxs-lookup"><span data-stu-id="09ab1-106">Templates overview</span></span>
<span data-ttu-id="09ab1-107">Azure Resource Manager 템플릿은 Azure 솔루션의 인프라와 구성을 정의하는 JSON 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="09ab1-107">Azure Resource Manager templates are JSON files that define the infrastructure and configuration of your Azure solution.</span></span> <span data-ttu-id="09ab1-108">템플릿을 사용하여 수명 주기 내내 솔루션을 반복적으로 배포하고 안심하고 일관된 상태로 리소스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09ab1-108">By using a template, you can repeatedly deploy your solution throughout its lifecycle and have confidence your resources are deployed in a consistent state.</span></span> <span data-ttu-id="09ab1-109">템플릿의 형식 및 템플릿을 생성하는 방법에 대해 자세히 알아보려면 [첫 번째 Azure Resource Manager 템플릿 만들기](../../azure-resource-manager/resource-manager-create-first-template.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09ab1-109">To learn more about the format of the template and how you construct it, see [Create your first Azure Resource Manager template](../../azure-resource-manager/resource-manager-create-first-template.md).</span></span> <span data-ttu-id="09ab1-110">리소스 유형의 JSON 구문을 보려면 [Azure Resource Manager 템플릿에서 리소스 정의](/azure/templates/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09ab1-110">To view the JSON syntax for resources types, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span>


## <a name="create-resource-group"></a><span data-ttu-id="09ab1-111">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="09ab1-111">Create resource group</span></span>
<span data-ttu-id="09ab1-112">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="09ab1-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="09ab1-113">가상 컴퓨터보다 먼저 리소스 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09ab1-113">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="09ab1-114">다음 예제에서는 *eastus* 지역에 *myResourceGroupVM*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09ab1-114">The following example creates a resource group named *myResourceGroupVM* in the *eastus* region:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="09ab1-115">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="09ab1-115">Create virtual machine</span></span>
<span data-ttu-id="09ab1-116">다음 예제에서는 [az group deployment create](/cli/azure/group/deployment#create)를 사용하여 [이 Azure Resource Manager 템플릿](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json)에서 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09ab1-116">The following example creates a VM from [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="09ab1-117">*~/.ssh/id_rsa.pub*의 내용과 같은 고유한 SSH 공용 키의 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="09ab1-117">Provide the value of your own SSH public key, such as the contents of *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="09ab1-118">SSH 키 쌍을 만들어야 하는 경우 [Azure에서 Linux VM용 SSH 키 쌍을 만들고 사용하는 방법](mac-create-ssh-keys.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09ab1-118">If you need to create an SSH key pair, see [How to create and use an SSH key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

<span data-ttu-id="09ab1-119">이 예제에서는 GitHub에 저장된 템플릿을 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="09ab1-119">In this example, you specified a template stored in GitHub.</span></span> <span data-ttu-id="09ab1-120">또한 템플릿을 다운로드하거나 만들고 동일한 `--template-file` 매개 변수로 로컬 경로를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09ab1-120">You can also download or create a template and specify the local path with the same `--template-file` parameter.</span></span>

<span data-ttu-id="09ab1-121">VM에 SSH하려면 [az network public-ip show](/cli/azure/network/public-ip#show)를 사용하여 공용 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="09ab1-121">To SSH to your VM, obtain the public IP address with [az network public-ip show](/cli/azure/network/public-ip#show):</span></span>

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="09ab1-122">그런 다음 정상적으로 VM에 SSH할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09ab1-122">You can then SSH to your VM as normal:</span></span>

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a><span data-ttu-id="09ab1-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="09ab1-123">Next steps</span></span>
<span data-ttu-id="09ab1-124">이 예제에서는 기본 Linux VM을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="09ab1-124">In this example, you created a basic Linux VM.</span></span> <span data-ttu-id="09ab1-125">응용 프로그램 프레임워크를 포함하거나 더 복잡한 환경을 만드는 더 많은 Resource Manager 템플릿은 [Azure 빠른 시작 템플릿 갤러리](https://azure.microsoft.com/documentation/templates/)를 찾아보세요.</span><span class="sxs-lookup"><span data-stu-id="09ab1-125">For more Resource Manager templates that include application frameworks or create more complex environments, browse the [Azure quickstart templates gallery](https://azure.microsoft.com/documentation/templates/).</span></span>