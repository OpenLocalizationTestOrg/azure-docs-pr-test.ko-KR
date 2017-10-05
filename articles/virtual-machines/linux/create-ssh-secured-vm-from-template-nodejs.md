---
title: "Azure CLI 1.0과 함께 Azure 템플릿을 사용하여 Linux VM 만들기 | Microsoft Docs"
description: "Azure CLI 1.0 및 Azure Resource Manager 템플릿을 사용하여 Azure에 Linux VM을 만듭니다."
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
ms.openlocfilehash: 33d4aaa78fcdf3bd9e2e236606f2d3049f464a8a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-linux-vm-using-the-azure-cli-10-an-azure-resource-manager-template"></a><span data-ttu-id="994c6-103">Azure CLI 1.0 및 Azure Resource Manager 템플릿을 사용하여 Linux VM을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="994c6-103">How to create a Linux VM using the Azure CLI 1.0 an Azure Resource Manager template</span></span>
<span data-ttu-id="994c6-104">이 문서에서는 Azure CLI 1.0 및 Azure Resource Manager 템플릿을 사용하여 Linux 가상 컴퓨터를 신속하게 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="994c6-104">This article shows you how to quickly deploy a Linux Virtual Machine using the Azure CLI 1.0 and an Azure Resource Manager template.</span></span> <span data-ttu-id="994c6-105">이 문서의 내용을 실행하기 위해 필요한 사항:</span><span class="sxs-lookup"><span data-stu-id="994c6-105">The article requires:</span></span>

* <span data-ttu-id="994c6-106">Azure 계정([무료 평가판 받기](https://azure.microsoft.com/pricing/free-trial/))</span><span class="sxs-lookup"><span data-stu-id="994c6-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="994c6-107">`azure login`으로 로그인된 [Azure CLI 1.0](../../cli-install-nodejs.md)</span><span class="sxs-lookup"><span data-stu-id="994c6-107">the [Azure CLI 1.0](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="994c6-108">Azure Resource Manager 모드 `azure config mode arm`으로 *있어야 하는* Azure CLI</span><span class="sxs-lookup"><span data-stu-id="994c6-108">the Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

<span data-ttu-id="994c6-109">[Azure 포털](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 사용하여 Linux VM을 신속히 배포할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="994c6-109">You can also quickly deploy a Linux VM template by using the [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="994c6-110">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="994c6-110">CLI versions to complete the task</span></span>
<span data-ttu-id="994c6-111">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="994c6-111">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="994c6-112">[Azure CLI 1.0](#quick-command-summary) - 클래식 및 리소스 관리 배포 모델용 CLI(이 문서)</span><span class="sxs-lookup"><span data-stu-id="994c6-112">[Azure CLI 1.0](#quick-command-summary) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="994c6-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) - 리소스 관리 배포 모델용 차세대 CLI</span><span class="sxs-lookup"><span data-stu-id="994c6-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="994c6-114">빠른 명령 요약</span><span class="sxs-lookup"><span data-stu-id="994c6-114">Quick Command Summary</span></span>
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="994c6-115">자세한 연습</span><span class="sxs-lookup"><span data-stu-id="994c6-115">Detailed Walkthrough</span></span>
<span data-ttu-id="994c6-116">템플릿을 사용하면 사용자 이름 및 호스트 이름과 같은 시작 작업 중에 사용자 지정하려는 설정으로 Azure에서 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="994c6-116">Templates allow you to create VMs on Azure with settings that you want to customize during the launch, settings like usernames and hostnames.</span></span> <span data-ttu-id="994c6-117">이 문서의 경우 SSH에 오픈된 포트 22를 포함한 NSG(네트워크 보안 그룹)와 함께 Ubuntu VM을 활용하여 Azure 템플릿을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="994c6-117">For this article, we are launching an Azure template utilizing an Ubuntu VM along with a network security group (NSG) with port 22 open for SSH.</span></span>

<span data-ttu-id="994c6-118">Azure Resource Manager 템플릿은 이 문서에서와 같이 Ubuntu VM을 시작하는 등 간단한 일회성 작업에 사용할 수 있는 JSON 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="994c6-118">Azure Resource Manager templates are JSON files that can be used for simple one-off tasks like launching an Ubuntu VM as done in this article.</span></span>  <span data-ttu-id="994c6-119">Azure 템플릿은 테스트, 개발 또는 프로덕션 배포 스택처럼 전체 환경의 복잡한 Azure 구성을 만드는 데도 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="994c6-119">Azure Templates can also be used to construct complex Azure configurations of entire environments like a testing, dev, or production deployment stack.</span></span>

## <a name="create-the-linux-vm"></a><span data-ttu-id="994c6-120">Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="994c6-120">Create the Linux VM</span></span>
<span data-ttu-id="994c6-121">다음 코드 예제에서는 `azure group create`를 호출하여 [이 Azure Resource Manager 템플릿](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json)을 사용하여 리소스 그룹을 만드는 동시에 SSH 보안 Linux VM을 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="994c6-121">The following code example shows how to call `azure group create` to create a resource group and deploy an SSH-secured Linux VM at the same time using [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span></span> <span data-ttu-id="994c6-122">예제에서 환경에 고유한 이름을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="994c6-122">Remember that in your example you need to use names that are unique to your environment.</span></span> <span data-ttu-id="994c6-123">이 예제에서는 *myResourceGroup*을 리소스 그룹 이름으로, *myVM*을 VM 이름으로 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="994c6-123">This example uses *myResourceGroup* as the resource group name, and *myVM* as the VM name.</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

<span data-ttu-id="994c6-124">출력에는 다음과 같은 출력 블록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="994c6-124">The output should look like the following output block:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for the following parameters
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

<span data-ttu-id="994c6-125">해당 예에서는 `--template-uri` 매개 변수를 사용하여 VM을 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="994c6-125">That example deployed a VM using the `--template-uri` parameter.</span></span>  <span data-ttu-id="994c6-126">인수인 템플릿 파일에 대한 경로가 있는 `--template-file` 매개 변수를 사용하여 템플릿을 다운로드하거나 로컬로 만들고 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="994c6-126">You can also download or create a template locally and pass the template using the `--template-file` parameter with a path to the template file as an argument.</span></span> <span data-ttu-id="994c6-127">Azure CLI는 템플릿에서 필요한 매개 변수에 대한 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="994c6-127">The Azure CLI prompts you for the parameters required by the template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="994c6-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="994c6-128">Next steps</span></span>
<span data-ttu-id="994c6-129">[템플릿 갤러리](https://azure.microsoft.com/documentation/templates/) 를 검색하여 다음에 배포할 앱 프레임워크를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="994c6-129">Search the [templates gallery](https://azure.microsoft.com/documentation/templates/) to discover what app frameworks to deploy next.</span></span>

