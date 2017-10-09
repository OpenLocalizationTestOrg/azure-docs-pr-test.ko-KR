---
title: "Azure에서 Linux VM 전체 aaaUse Ansible toocreate | Microsoft Docs"
description: "자세한 내용은 방법 toouse Ansible toocreate 전체 Azure에서 Linux 가상 컴퓨터 환경 관리"
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
ms.openlocfilehash: 970b0427f39fc23240f9faab868196ca4f444e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-environment-in-azure-with-ansible"></a><span data-ttu-id="5ace8-103">Azure에서 Ansible을 사용하여 전체 Linux 가상 컴퓨터 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="5ace8-103">Create a complete Linux virtual machine environment in Azure with Ansible</span></span>
<span data-ttu-id="5ace8-104">Ansible 있습니다 tooautomate hello 배포 및 구성 리소스의 사용자 환경에서.</span><span class="sxs-lookup"><span data-stu-id="5ace8-104">Ansible allows you tooautomate hello deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="5ace8-105">Azure에서 가상 컴퓨터 (Vm) Ansible toomanage을 사용 하 여, 다른 리소스와 마찬가지로 동일한 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace8-105">You can use Ansible toomanage your virtual machines (VMs) in Azure, hello same as you would any other resource.</span></span> <span data-ttu-id="5ace8-106">이 문서에서는 어떻게 toocreate 완벽 한 Linux 환경 및 Ansible 사용 하 여 리소스를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace8-106">This article shows you how toocreate a complete Linux environment and supporting resources with Ansible.</span></span> <span data-ttu-id="5ace8-107">배울 수 있습니다 어떻게 너무[Ansible 기본 VM 만들기](ansible-create-vm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace8-107">You can also learn how too[Create a basic VM with Ansible](ansible-create-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="5ace8-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5ace8-108">Prerequisites</span></span>
<span data-ttu-id="5ace8-109">Azure toomanage Ansible 사용 하 여 리소스를 해야 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="5ace8-109">toomanage Azure resources with Ansible, you need hello following:</span></span>

- <span data-ttu-id="5ace8-110">Ansible 호스트 시스템에 설치 된 Azure Python SDK 모듈 hello 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace8-110">Ansible and hello Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="5ace8-111">[Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) 및 [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)에 Ansible 설치</span><span class="sxs-lookup"><span data-stu-id="5ace8-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="5ace8-112">Azure 자격 증명 및 구성 Ansible toouse 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace8-112">Azure credentials, and Ansible configured toouse them.</span></span>
    - [<span data-ttu-id="5ace8-113">Azure 자격 증명 만들기 및 Ansible 구성</span><span class="sxs-lookup"><span data-stu-id="5ace8-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="5ace8-114">Azure CLI 버전 2.0.4 이상</span><span class="sxs-lookup"><span data-stu-id="5ace8-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="5ace8-115">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="5ace8-115">Run `az --version` toofind hello version.</span></span> 
    - <span data-ttu-id="5ace8-116">Tooupgrade 필요한 경우 참조 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace8-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="5ace8-117">또한 브라우저에서 [Cloud Shell](/azure/cloud-shell/quickstart)을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace8-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-virtual-network"></a><span data-ttu-id="5ace8-118">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="5ace8-118">Create virtual network</span></span>
<span data-ttu-id="5ace8-119">hello는 Ansible 플레이 북의 다음 섹션 가상 네트워크를 만들어 명명 된 *myVnet* hello에 *10.0.0.0/16* 주소 공간:</span><span class="sxs-lookup"><span data-stu-id="5ace8-119">hello following section in an Ansible playbook creates a virtual network named *myVnet* in hello *10.0.0.0/16* address space:</span></span>

```yaml
- name: Create virtual network
  azure_rm_virtualnetwork:
    resource_group: myResourceGroup
    name: myVnet
    address_prefixes: "10.10.0.0/16"
```

<span data-ttu-id="5ace8-120">서브넷 tooadd 다음 단원을 hello 이라는 서브넷을 만듭니다. *mySubnet* hello에 *myVnet* 가상 네트워크:</span><span class="sxs-lookup"><span data-stu-id="5ace8-120">tooadd a subnet, hello following section creates a subnet named *mySubnet* in hello *myVnet* virtual network:</span></span>

```yaml
- name: Add subnet
  azure_rm_subnet:
    resource_group: myResourceGroup
    name: mySubnet
    address_prefix: "10.0.1.0/24"
    virtual_network: myVnet
```


## <a name="create-public-ip-address"></a><span data-ttu-id="5ace8-121">공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="5ace8-121">Create public IP address</span></span>
<span data-ttu-id="5ace8-122">hello 인터넷을 통해 tooaccess 리소스 만들고 공용 IP 주소 tooyour VM을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace8-122">tooaccess resources across hello Internet, create and assign a public IP address tooyour VM.</span></span> <span data-ttu-id="5ace8-123">hello는 Ansible 플레이 북의 다음 섹션 공용 IP 주소를 만들고 명명 된 *myPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="5ace8-123">hello following section in an Ansible playbook creates a public IP address named *myPublicIP*:</span></span>

```yaml
- name: Create public IP address
  azure_rm_publicipaddress:
    resource_group: myResourceGroup
    allocation_method: Static
    name: myPublicIP
```


## <a name="create-network-security-group"></a><span data-ttu-id="5ace8-124">네트워크 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="5ace8-124">Create Network Security Group</span></span>
<span data-ttu-id="5ace8-125">네트워크 보안 그룹 VM 내부 및 외부 네트워크 트래픽의 hello 흐름을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace8-125">Network Security Groups control hello flow of network traffic in and out of your VM.</span></span> <span data-ttu-id="5ace8-126">hello 다음 섹션에는 Ansible 플레이 북 네트워크 보안 그룹을 만듭니다 라는 *myNetworkSecurityGroup* 하 고 TCP 포트 22에서 규칙 tooallow SSH 트래픽 정의:</span><span class="sxs-lookup"><span data-stu-id="5ace8-126">hello following section in an Ansible playbook creates a network security group named *myNetworkSecurityGroup* and defines a rule tooallow SSH traffic on TCP port 22:</span></span>

```yaml
- name: Create Network Security Group that allows SSH
  azure_rm_securitygroup:
    resource_group: myResourceGroup
    name: myNetworkSecurityGroup
    rules:
      - name: SSH
        protocol: TCP
        destination_port_range: 22
        access: Allow
        priority: 1001
        direction: Inbound
```


## <a name="create-virtual-network-interface-card"></a><span data-ttu-id="5ace8-127">가상 네트워크 인터페이스 카드 만들기</span><span class="sxs-lookup"><span data-stu-id="5ace8-127">Create virtual network interface card</span></span>
<span data-ttu-id="5ace8-128">가상 네트워크 인터페이스 카드 (NIC) 가상 네트워크, 공용 IP 주소 및 네트워크 보안 그룹을 지정 하 여 VM tooa를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace8-128">A virtual network interface card (NIC) connects your VM tooa given virtual network, public IP address, and network security group.</span></span> <span data-ttu-id="5ace8-129">hello는 Ansible 플레이 북의 다음 섹션을 만듭니다 라는 가상 NIC *myNIC* 만든 toohello 가상 네트워킹 리소스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace8-129">hello following section in an Ansible playbook creates a virtual NIC named *myNIC* connected toohello virtual networking resources you have created:</span></span>

```yaml
- name: Create virtual network inteface card
  azure_rm_networkinterface:
    resource_group: myResourceGroup
    name: myNIC
    virtual_network: myVnet
    subnet: mySubnet
    public_ip_name: myPublicIP
    security_group: myNetworkSecurityGroup
```


## <a name="create-virtual-machine"></a><span data-ttu-id="5ace8-130">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="5ace8-130">Create virtual machine</span></span>
<span data-ttu-id="5ace8-131">hello 마지막 단계가 toocreate VM 및 생성 된 모든 hello 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace8-131">hello final step is toocreate a VM and use all hello resources created.</span></span> <span data-ttu-id="5ace8-132">hello는 Ansible 플레이 북의 다음 섹션을 만듭니다 라는 VM *myVM* 연결 합니다. 명명 된 가상 NIC hello 및 *myNIC*합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace8-132">hello following section in an Ansible playbook creates a VM named *myVM* and attaches hello virtual NIC named *myNIC*.</span></span> <span data-ttu-id="5ace8-133">Hello에 공용 키 데이터를 입력 *key_data* 다음과 같이 쌍으로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace8-133">Enter your own public key data in hello *key_data* pair as follows:</span></span>

```yaml
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
    network_interfaces: myNIC
    image:
      offer: CentOS
      publisher: OpenLogic
      sku: '7.3'
      version: latest
```

## <a name="complete-ansible-playbook"></a><span data-ttu-id="5ace8-134">전체 Ansible Playbook</span><span class="sxs-lookup"><span data-stu-id="5ace8-134">Complete Ansible playbook</span></span>
<span data-ttu-id="5ace8-135">toobring 만들 라는 Ansible 플레이 북 함께이 섹션에서는 모든 *azure_create_complete_vm.yml* 붙여넣기 hello 내용에 따라:</span><span class="sxs-lookup"><span data-stu-id="5ace8-135">toobring all these sections together, create an Ansible playbook named *azure_create_complete_vm.yml* and paste hello following contents:</span></span>

```yaml
- name: Create Azure VM
  hosts: localhost
  connection: local
  tasks:
  - name: Create virtual network
    azure_rm_virtualnetwork:
      resource_group: myResourceGroup
      name: myVnet
      address_prefixes: "10.0.0.0/16"
  - name: Add subnet
    azure_rm_subnet:
      resource_group: myResourceGroup
      name: mySubnet
      address_prefix: "10.0.1.0/24"
      virtual_network: myVnet
  - name: Create public IP address
    azure_rm_publicipaddress:
      resource_group: myResourceGroup
      allocation_method: Static
      name: myPublicIP
  - name: Create Network Security Group that allows SSH
    azure_rm_securitygroup:
      resource_group: myResourceGroup
      name: myNetworkSecurityGroup
      rules:
        - name: SSH
          protocol: Tcp
          destination_port_range: 22
          access: Allow
          priority: 1001
          direction: Inbound
  - name: Create virtual network inteface card
    azure_rm_networkinterface:
      resource_group: myResourceGroup
      name: myNIC
      virtual_network: myVnet
      subnet: mySubnet
      public_ip_name: myPublicIP
      security_group: myNetworkSecurityGroup
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
      network_interfaces: myNIC
      image:
        offer: CentOS
        publisher: OpenLogic
        sku: '7.3'
        version: latest
```

<span data-ttu-id="5ace8-136">Ansible에 모든 리소스를 리소스 그룹 toodeploy 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace8-136">Ansible needs a resource group toodeploy all your resources into.</span></span> <span data-ttu-id="5ace8-137">[az group create](/cli/azure/vm#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ace8-137">Create a resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="5ace8-138">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치:</span><span class="sxs-lookup"><span data-stu-id="5ace8-138">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="5ace8-139">toocreate hello 완료 VM 환경과 Ansible, hello 플레이 북을 다음과 같이 실행:</span><span class="sxs-lookup"><span data-stu-id="5ace8-139">toocreate hello complete VM environment with Ansible, run hello playbook as follows:</span></span>

```bash
ansible-playbook azure_create_complete_vm.yml
```

<span data-ttu-id="5ace8-140">hello 출력은 다음 VM 성공적으로 만들었습니다. hello를 보여 주는 예제와 비슷한 toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace8-140">hello output looks similar toohello following example that shows hello VM has been successfully created:</span></span>

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create virtual network] *********************************************
changed: [localhost]

TASK [Add subnet] *********************************************************
changed: [localhost]

TASK [Create public IP address] *******************************************
changed: [localhost]

TASK [Create Network Security Group that allows SSH] **********************
changed: [localhost]

TASK [Create virtual network inteface card] *******************************
changed: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=7    changed=6    unreachable=0    failed=0
```

## <a name="next-steps"></a><span data-ttu-id="5ace8-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5ace8-141">Next steps</span></span>
<span data-ttu-id="5ace8-142">이 예제에는 필요한 hello 가상 네트워킹 리소스를 포함 하 여 완벽 한 VM 환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ace8-142">This example creates a complete VM environment including hello required virtual networking resources.</span></span> <span data-ttu-id="5ace8-143">직접적 예제 toocreate 기본 옵션으로 기존 네트워크 리소스에 VM 참조 하십시오. [VM을 만들](ansible-create-vm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace8-143">For a more direct example toocreate a VM into existing network resources with default options, see [Create a VM](ansible-create-vm.md).</span></span>
