---
title: "Azure에서 Ansible을 사용하여 기본 Linux VM 만들기 | Microsoft Docs"
description: "Azure에서 Ansible을 사용하여 기본 Linux 가상 컴퓨터를 만들고 관리하는 방법을 알아봅니다"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/25/2017
ms.author: iainfou
ms.openlocfilehash: 526f3522334450564500c4ba0e401a683cae55f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a><span data-ttu-id="24d7c-103">Azure에서 Ansible을 사용하여 기본 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="24d7c-103">Create a basic virtual machine in Azure with Ansible</span></span>
<span data-ttu-id="24d7c-104">Ansible을 사용하면 사용자 환경에서 리소스의 배포 및 구성을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d7c-104">Ansible allows you to automate the deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="24d7c-105">Azure에서 Ansible을 사용하여 다른 리소스와 동일한 방식으로 VM(가상 컴퓨터)을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d7c-105">You can use Ansible to manage your virtual machines (VMs) in Azure, the same as you would any other resource.</span></span> <span data-ttu-id="24d7c-106">이 문서에서는 Ansible을 사용하여 기본 VM을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="24d7c-106">This article shows you how to create a basic VM with Ansible.</span></span> <span data-ttu-id="24d7c-107">또한 [Ansible을 사용하여 전체 VM 환경을 만드는](ansible-create-complete-vm.md) 방법도 배울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d7c-107">You can also learn how to [Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="24d7c-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="24d7c-108">Prerequisites</span></span>
<span data-ttu-id="24d7c-109">Ansible을 사용하여 Azure 리소스를 관리하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="24d7c-109">To manage Azure resources with Ansible, you need the following:</span></span>

- <span data-ttu-id="24d7c-110">호스트 시스템에 설치된 Ansible 및 Azure Python SDK 모듈</span><span class="sxs-lookup"><span data-stu-id="24d7c-110">Ansible and the Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="24d7c-111">[Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) 및 [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)에 Ansible 설치</span><span class="sxs-lookup"><span data-stu-id="24d7c-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="24d7c-112">Azure 자격 증명 및 이를 사용하도록 구성된 Ansible</span><span class="sxs-lookup"><span data-stu-id="24d7c-112">Azure credentials, and Ansible configured to use them.</span></span>
    - [<span data-ttu-id="24d7c-113">Azure 자격 증명 만들기 및 Ansible 구성</span><span class="sxs-lookup"><span data-stu-id="24d7c-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="24d7c-114">Azure CLI 버전 2.0.4 이상</span><span class="sxs-lookup"><span data-stu-id="24d7c-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="24d7c-115">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="24d7c-115">Run `az --version` to find the version.</span></span> 
    - <span data-ttu-id="24d7c-116">업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24d7c-116">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="24d7c-117">또한 브라우저에서 [Cloud Shell](/azure/cloud-shell/quickstart)을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d7c-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-supporting-azure-resources"></a><span data-ttu-id="24d7c-118">지원 Azure 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="24d7c-118">Create supporting Azure resources</span></span>
<span data-ttu-id="24d7c-119">이 예제에서는 기존 인프라에 VM을 배포하는 runbook을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24d7c-119">In this example, we create a runbook that deploys a VM into an existing infrastructure.</span></span> <span data-ttu-id="24d7c-120">먼저 [az group create](/cli/azure/vm#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24d7c-120">First, create resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="24d7c-121">다음 예제에서는 *eastus* 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24d7c-121">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="24d7c-122">[az network vnet create](/cli/azure/network/vnet#create)를 사용하여 VM의 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24d7c-122">Create a virtual network for your VM with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="24d7c-123">다음 예제에서는 *myVnet*이라는 가상 네트워크와 *mySubnet*이라는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24d7c-123">The following example creates a virtual network named *myVnet* and a subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a><span data-ttu-id="24d7c-124">Ansible Playbook 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="24d7c-124">Create and run Ansible playbook</span></span>
<span data-ttu-id="24d7c-125">**azure_create_vm.yml**이라는 Ansible Playbook을 만들고 다음 내용을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="24d7c-125">Create an Ansible playbook named **azure_create_vm.yml** and paste the following contents.</span></span> <span data-ttu-id="24d7c-126">이 예제에서는 단일 VM을 만들고 SSH 자격 증명을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="24d7c-126">This example creates a single VM and configures SSH credentials.</span></span> <span data-ttu-id="24d7c-127">다음과 같이 *key_data* 쌍으로 사용자 고유의 공개 키 데이터를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="24d7c-127">Enter your own public key data in the *key_data* pair as follows:</span></span>

```yaml
- name: Create Azure VM
  hosts: localhost
  connection: local
  tasks:
  - name: Create VM
    azure_rm_virtualmachine:
      resource_group: myResourceGroup
      name: myVM
      vm_size: Standard_DS1_v2
      admin_username: azureuser
      ssh_password_enabled: false
      ssh_public_keys: 
        - path: /home/azureuser/.ssh/authorized_keys
          key_data: "ssh-rsa AAAAB3Nz{snip}hwhqT9h"
      image:
        offer: CentOS
        publisher: OpenLogic
        sku: '7.3'
        version: latest
```

<span data-ttu-id="24d7c-128">Ansible을 사용하여 VM을 만들려면 다음과 같이 Playbook을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="24d7c-128">To create the VM with Ansible, run the playbook as follows:</span></span>

```bash
ansible-playbook azure_create_vm.yml
```

<span data-ttu-id="24d7c-129">출력은 VM이 성공적으로 만들어졌음을 보여 주는 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="24d7c-129">The output looks similar to the following example that shows the VM has been successfully created:</span></span>

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a><span data-ttu-id="24d7c-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="24d7c-130">Next steps</span></span>
<span data-ttu-id="24d7c-131">이 예제에서는 기존 리소스 그룹에 VM을 만들고 이미 배포된 가상 네트워크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24d7c-131">This example creates a VM in an existing resource group and with a virtual network already deployed.</span></span> <span data-ttu-id="24d7c-132">Ansible을 사용하여 가상 네트워크 및 네트워크 보안 그룹 규칙 등의 지원 리소스를 만드는 방법에 대한 자세한 예제는 [Ansible을 사용하여 전체 VM 환경 만들기](ansible-create-complete-vm.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24d7c-132">For a more detailed example on how to use Ansible to create supporting resources such as a virtual network and Network Security Group rules, see [Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>