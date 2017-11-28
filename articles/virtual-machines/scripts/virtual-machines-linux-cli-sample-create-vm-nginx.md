---
title: "Azure CLI 스크립트 샘플 - NGINX를 사용하여 Linux VM 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - NGINX를 사용하여 Linux VM 만들기"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 416624d9e378d09f4fb0593119dbc30adeb09f91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-nginx"></a><span data-ttu-id="45484-103">NGINX를 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="45484-103">Create a VM with NGINX</span></span>

<span data-ttu-id="45484-104">이 스크립트는 Azure Virtual Machine을 만들고 Azure Virtual Machine 사용자 지정 스크립트 확장을 사용하여 NGINX를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="45484-104">This script creates an Azure Virtual Machine and uses the Azure Virtual Machine Custom Script Extension to install NGINX.</span></span> <span data-ttu-id="45484-105">스크립트를 실행하면 가상 컴퓨터의 공용 IP 주소에서 데모 웹 사이트에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45484-105">After running the script, you can access a demo website on the public IP address of the virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="45484-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="45484-106">Sample script</span></span>

<span data-ttu-id="45484-107">[!code-azurecli-interactive[기본](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "VM 빠른 생성")]</span><span class="sxs-lookup"><span data-stu-id="45484-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]</span></span>

## <a name="custom-script-extension"></a><span data-ttu-id="45484-108">사용자 지정 스크립트 확장</span><span class="sxs-lookup"><span data-stu-id="45484-108">Custom Script Extension</span></span>

<span data-ttu-id="45484-109">사용자 지정 스크립트 확장은 가상 컴퓨터에 이 스크립트를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="45484-109">The custom script extension copies this script onto the virtual machine.</span></span> <span data-ttu-id="45484-110">그런 다음 스크립트를 실행하여 NGINX 웹 서버를 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="45484-110">The script is then run to install and configure an NGINX web server.</span></span> 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="clean-up-deployment"></a><span data-ttu-id="45484-111">배포 정리</span><span class="sxs-lookup"><span data-stu-id="45484-111">Clean up deployment</span></span> 

<span data-ttu-id="45484-112">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45484-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="45484-113">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="45484-113">Script explanation</span></span>

<span data-ttu-id="45484-114">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 가상 컴퓨터 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45484-114">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="45484-115">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="45484-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="45484-116">명령</span><span class="sxs-lookup"><span data-stu-id="45484-116">Command</span></span> | <span data-ttu-id="45484-117">참고 사항</span><span class="sxs-lookup"><span data-stu-id="45484-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="45484-118">az group create</span><span class="sxs-lookup"><span data-stu-id="45484-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="45484-119">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45484-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="45484-120">az vm create</span><span class="sxs-lookup"><span data-stu-id="45484-120">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="45484-121">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45484-121">Creates the virtual machine.</span></span> <span data-ttu-id="45484-122">또한 이 명령은 사용할 가상 컴퓨터 이미지와 관리 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="45484-122">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="45484-123">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="45484-123">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="45484-124">인바운드 트래픽을 허용하도록 네트워크 보안 그룹 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45484-124">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="45484-125">이 샘플에서 HTTP 트래픽에 대해 포트 80이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="45484-125">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="45484-126">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="45484-126">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="45484-127">VM에 가상 컴퓨터 확장을 추가하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="45484-127">Adds and runs a virtual machine extension to a VM.</span></span> <span data-ttu-id="45484-128">이 샘플에서 사용자 지정 스크립트 확장은 NGINX를 설치하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="45484-128">In this sample, the custom script extension is used to install NGINX.</span></span>|
| [<span data-ttu-id="45484-129">az group delete</span><span class="sxs-lookup"><span data-stu-id="45484-129">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="45484-130">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="45484-130">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="45484-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="45484-131">Next steps</span></span>

<span data-ttu-id="45484-132">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45484-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="45484-133">추가 가상 컴퓨터 CLI 스크립트 샘플은 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45484-133">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
