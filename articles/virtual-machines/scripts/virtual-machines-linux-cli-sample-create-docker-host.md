---
title: "aaaAzure CLI 스크립트 샘플-Docker 호스트 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Docker 호스트 만들기"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7df2561c428ff5d3ab0a0d53c8e046781996be77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-docker"></a><span data-ttu-id="1493b-103">Docker를 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="1493b-103">Create a VM with Docker</span></span>

<span data-ttu-id="1493b-104">이 스크립트는 Docker를 사용하는 가상 컴퓨터를 만들고 Docker 컨테이너에서 NGINX를 실행하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1493b-104">This script creates a virtual machine with Docker enabled and starts a Docker container running NGINX.</span></span> <span data-ttu-id="1493b-105">Hello 스크립트를 실행 한 후 hello NGINX 웹 서버 hello hello Azure 가상 컴퓨터의 FQDN 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1493b-105">After running hello script, you can access hello NGINX web server through hello FQDN of hello Azure virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1493b-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="1493b-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-docker-host/create-docker-host.sh "Docker Host")]

## <a name="clean-up-deployment"></a><span data-ttu-id="1493b-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="1493b-107">Clean up deployment</span></span> 

<span data-ttu-id="1493b-108">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1493b-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="1493b-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="1493b-109">Script explanation</span></span>

<span data-ttu-id="1493b-110">이 스크립트 명령 toocreate hello 배포한 후에 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1493b-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="1493b-111">Hello 테이블의 각 항목 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1493b-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1493b-112">명령</span><span class="sxs-lookup"><span data-stu-id="1493b-112">Command</span></span> | <span data-ttu-id="1493b-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="1493b-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1493b-114">az group create</span><span class="sxs-lookup"><span data-stu-id="1493b-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="1493b-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1493b-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1493b-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="1493b-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="1493b-117">Hello 가상 컴퓨터를 만들고 toohello 네트워크 카드, 가상 네트워크, 서브넷 및 네트워크 보안 그룹을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1493b-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="1493b-118">이 명령은 hello 가상 컴퓨터 이미지 toobe 사용 및 관리 자격 증명에도 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1493b-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="1493b-119">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="1493b-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="1493b-120">네트워크 보안 그룹 규칙 tooallow 만듭니다 트래픽 인바운드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1493b-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="1493b-121">이 샘플에서 HTTP 트래픽에 대해 포트 80이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="1493b-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="1493b-122">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="1493b-122">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="1493b-123">추가 하 고 가상 컴퓨터 확장 tooa VM을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1493b-123">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="1493b-124">이 샘플에서는 hello Docker VM 확장은 사용 되는 tooconfigure Docker 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="1493b-124">In this sample, hello Docker VM extension is used tooconfigure a Docker host.</span></span>|
| [<span data-ttu-id="1493b-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="1493b-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="1493b-126">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="1493b-126">Deletes a resource group, including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1493b-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1493b-127">Next steps</span></span>

<span data-ttu-id="1493b-128">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="1493b-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1493b-129">가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="1493b-129">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
