---
title: "CLI 스크립트 샘플-aaaAzure NGINX Linux VM 만들기 | Microsoft Docs"
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
ms.openlocfilehash: 9166ccfd4f2e6eea731a8dc6956575d9f8f85488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-nginx"></a><span data-ttu-id="05b38-103">NGINX를 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="05b38-103">Create a VM with NGINX</span></span>

<span data-ttu-id="05b38-104">이 스크립트는 Azure 가상 컴퓨터를 만들고 Azure 가상 컴퓨터 사용자 지정 스크립트 확장 tooinstall NGINX hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="05b38-104">This script creates an Azure Virtual Machine and uses hello Azure Virtual Machine Custom Script Extension tooinstall NGINX.</span></span> <span data-ttu-id="05b38-105">Hello 스크립트를 실행 한 후 hello hello 가상 컴퓨터의 공용 IP 주소에서 데모 웹 사이트를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05b38-105">After running hello script, you can access a demo website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="05b38-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="05b38-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]

## <a name="custom-script-extension"></a><span data-ttu-id="05b38-107">사용자 지정 스크립트 확장</span><span class="sxs-lookup"><span data-stu-id="05b38-107">Custom Script Extension</span></span>

<span data-ttu-id="05b38-108">사용자 지정 스크립트 확장 hello hello 가상 컴퓨터에이 스크립트를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="05b38-108">hello custom script extension copies this script onto hello virtual machine.</span></span> <span data-ttu-id="05b38-109">hello 스크립트 tooinstall 그런 다음를 실행 하 고 NGINX 웹 서버를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="05b38-109">hello script is then run tooinstall and configure an NGINX web server.</span></span> 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="clean-up-deployment"></a><span data-ttu-id="05b38-110">배포 정리</span><span class="sxs-lookup"><span data-stu-id="05b38-110">Clean up deployment</span></span> 

<span data-ttu-id="05b38-111">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="05b38-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="05b38-112">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="05b38-112">Script explanation</span></span>

<span data-ttu-id="05b38-113">이 스크립트 명령 toocreate 리소스 그룹에서 가상 컴퓨터를 다음 hello를 사용 하 고 모든 관련 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="05b38-113">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="05b38-114">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="05b38-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="05b38-115">명령</span><span class="sxs-lookup"><span data-stu-id="05b38-115">Command</span></span> | <span data-ttu-id="05b38-116">참고 사항</span><span class="sxs-lookup"><span data-stu-id="05b38-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="05b38-117">az group create</span><span class="sxs-lookup"><span data-stu-id="05b38-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="05b38-118">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05b38-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="05b38-119">az vm create</span><span class="sxs-lookup"><span data-stu-id="05b38-119">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="05b38-120">Hello 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05b38-120">Creates hello virtual machine.</span></span> <span data-ttu-id="05b38-121">이 명령은 hello 가상 컴퓨터 이미지 toobe 사용 및 관리 자격 증명에도 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="05b38-121">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="05b38-122">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="05b38-122">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="05b38-123">네트워크 보안 그룹 규칙 tooallow 만듭니다 트래픽 인바운드 합니다.</span><span class="sxs-lookup"><span data-stu-id="05b38-123">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="05b38-124">이 샘플에서 HTTP 트래픽에 대해 포트 80이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="05b38-124">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="05b38-125">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="05b38-125">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="05b38-126">추가 하 고 가상 컴퓨터 확장 tooa VM을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="05b38-126">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="05b38-127">이 샘플에서는 hello 사용자 지정 스크립트 확장 사용 되는 tooinstall NGINX 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05b38-127">In this sample, hello custom script extension is used tooinstall NGINX.</span></span>|
| [<span data-ttu-id="05b38-128">az group delete</span><span class="sxs-lookup"><span data-stu-id="05b38-128">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="05b38-129">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="05b38-129">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="05b38-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="05b38-130">Next steps</span></span>

<span data-ttu-id="05b38-131">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="05b38-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="05b38-132">가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="05b38-132">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
