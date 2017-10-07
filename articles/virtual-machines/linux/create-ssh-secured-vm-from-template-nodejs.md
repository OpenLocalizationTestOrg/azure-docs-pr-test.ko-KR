---
title: "Azure 템플릿 Azure CLI 1.0과 함께 사용 하 여 Linux VM aaaCreate | Microsoft Docs"
description: "Hello Azure CLI 1.0 및 Azure 리소스 관리자 템플릿을 사용 하 여 Azure에서 Linux VM을 만듭니다."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: v-livech
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b694cc8247a8431b7ef4b24cc7dc2b4cdb9660ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-vm-using-hello-azure-cli-10-an-azure-resource-manager-template"></a><span data-ttu-id="e9e1b-103">어떻게 사용 하 여 Linux VM a toocreate hello Azure CLI 1.0 Azure 리소스 관리자 템플릿</span><span class="sxs-lookup"><span data-stu-id="e9e1b-103">How toocreate a Linux VM using hello Azure CLI 1.0 an Azure Resource Manager template</span></span>
<span data-ttu-id="e9e1b-104">이 문서에서는 tooquickly hello Azure CLI 1.0 및 Azure 리소스 관리자 템플릿을 사용 하 여 Linux 가상 컴퓨터를 배포 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e9e1b-104">This article shows you how tooquickly deploy a Linux Virtual Machine using hello Azure CLI 1.0 and an Azure Resource Manager template.</span></span> <span data-ttu-id="e9e1b-105">hello 문서에는 다음 사항이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e9e1b-105">hello article requires:</span></span>

* <span data-ttu-id="e9e1b-106">Azure 계정([무료 평가판 받기](https://azure.microsoft.com/pricing/free-trial/))</span><span class="sxs-lookup"><span data-stu-id="e9e1b-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="e9e1b-107">hello [Azure CLI 1.0](../../cli-install-nodejs.md) 로그인 한 `azure login`합니다.</span><span class="sxs-lookup"><span data-stu-id="e9e1b-107">hello [Azure CLI 1.0](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="e9e1b-108">hello Azure CLI *에 있어야* Azure Resource Manager 모드 `azure config mode arm`합니다.</span><span class="sxs-lookup"><span data-stu-id="e9e1b-108">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

<span data-ttu-id="e9e1b-109">Hello를 사용 하 여 Linux VM 템플릿을 신속 하 게 배포할 수 있습니다 [Azure 포털](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9e1b-109">You can also quickly deploy a Linux VM template by using hello [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="e9e1b-110">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="e9e1b-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="e9e1b-111">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9e1b-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="e9e1b-112">[Azure CLI 1.0](#quick-command-summary) – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)</span><span class="sxs-lookup"><span data-stu-id="e9e1b-112">[Azure CLI 1.0](#quick-command-summary) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="e9e1b-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한</span><span class="sxs-lookup"><span data-stu-id="e9e1b-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="e9e1b-114">빠른 명령 요약</span><span class="sxs-lookup"><span data-stu-id="e9e1b-114">Quick Command Summary</span></span>
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="e9e1b-115">자세한 연습</span><span class="sxs-lookup"><span data-stu-id="e9e1b-115">Detailed Walkthrough</span></span>
<span data-ttu-id="e9e1b-116">템플릿을 사용 하면 toocreate Vm Azure의 hello 시작, 같은 사용자 이름 및 호스트 이름을 설정 하는 동안 toocustomize 되도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9e1b-116">Templates allow you toocreate VMs on Azure with settings that you want toocustomize during hello launch, settings like usernames and hostnames.</span></span> <span data-ttu-id="e9e1b-117">이 문서의 경우 SSH에 오픈된 포트 22를 포함한 NSG(네트워크 보안 그룹)와 함께 Ubuntu VM을 활용하여 Azure 템플릿을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e9e1b-117">For this article, we are launching an Azure template utilizing an Ubuntu VM along with a network security group (NSG) with port 22 open for SSH.</span></span>

<span data-ttu-id="e9e1b-118">Azure Resource Manager 템플릿은 이 문서에서와 같이 Ubuntu VM을 시작하는 등 간단한 일회성 작업에 사용할 수 있는 JSON 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e9e1b-118">Azure Resource Manager templates are JSON files that can be used for simple one-off tasks like launching an Ubuntu VM as done in this article.</span></span>  <span data-ttu-id="e9e1b-119">Azure 템플릿 전체 환경 테스트, 개발, 또는 프로덕션 배포 스택 처럼 사용 되는 tooconstruct 복잡 한 Azure 구성 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9e1b-119">Azure Templates can also be used tooconstruct complex Azure configurations of entire environments like a testing, dev, or production deployment stack.</span></span>

## <a name="create-hello-linux-vm"></a><span data-ttu-id="e9e1b-120">Hello Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="e9e1b-120">Create hello Linux VM</span></span>
<span data-ttu-id="e9e1b-121">코드 예제에서 보여 주는 방법을 다음 hello toocall `azure group create` toocreate 리소스 그룹화 하 고 hello에는 SSH 보안 Linux VM을 배포할 사용 하 여 동일한 시간 [이 Azure 리소스 관리자 템플릿을](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9e1b-121">hello following code example shows how toocall `azure group create` toocreate a resource group and deploy an SSH-secured Linux VM at hello same time using [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span></span> <span data-ttu-id="e9e1b-122">고유한 tooyour 환경 있는 toouse 이름이 필요한 예에서 유의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9e1b-122">Remember that in your example you need toouse names that are unique tooyour environment.</span></span> <span data-ttu-id="e9e1b-123">이 예에서는 *myResourceGroup* hello 리소스 그룹 이름으로 및 *myVM* hello VM 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9e1b-123">This example uses *myResourceGroup* as hello resource group name, and *myVM* as hello VM name.</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

<span data-ttu-id="e9e1b-124">hello 출력은 출력 블록 뒤 hello 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9e1b-124">hello output should look like hello following output block:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for hello following parameters
sshKeyData: ssh-rsa AAAAB3Nza<..ssh public key text..>VQgwjNjQ== myAdminUser@myVM
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/<..subid text..>/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

<span data-ttu-id="e9e1b-125">그 예에서 hello를 사용 하는 VM 배포 `--template-uri` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="e9e1b-125">That example deployed a VM using hello `--template-uri` parameter.</span></span>  <span data-ttu-id="e9e1b-126">또한 또는 로컬로 템플릿을 만드는 있으며 hello를 사용 하 여 hello 템플릿을 전달 `--template-file` 매개 변수를 인수로 경로 toohello 템플릿 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9e1b-126">You can also download or create a template locally and pass hello template using hello `--template-file` parameter with a path toohello template file as an argument.</span></span> <span data-ttu-id="e9e1b-127">hello Azure CLI 매개 변수를 hello hello 템플릿에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9e1b-127">hello Azure CLI prompts you for hello parameters required by hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9e1b-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e9e1b-128">Next steps</span></span>
<span data-ttu-id="e9e1b-129">검색 hello [템플릿 갤러리](https://azure.microsoft.com/documentation/templates/) toodiscover 어떤 응용 프로그램 프레임 워크 toodeploy 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9e1b-129">Search hello [templates gallery](https://azure.microsoft.com/documentation/templates/) toodiscover what app frameworks toodeploy next.</span></span>

