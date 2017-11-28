---
title: "Azure에서 Ansible을 사용하여 전체 Linux VM 만들기 | Microsoft 문서"
description: "Azure에서 Ansible을 사용하여 전체 Linux 가상 컴퓨터 환경을 만들고 관리하는 방법을 알아봅니다"
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
ms.openlocfilehash: b2fcc288b40c12a9b3f966156ee2eedf4acca313
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-complete-linux-virtual-machine-environment-in-azure-with-ansible"></a><span data-ttu-id="c296a-103">Azure에서 Ansible을 사용하여 전체 Linux 가상 컴퓨터 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="c296a-103">Create a complete Linux virtual machine environment in Azure with Ansible</span></span>
<span data-ttu-id="c296a-104">Ansible을 사용하면 사용자 환경에서 리소스의 배포 및 구성을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c296a-104">Ansible allows you to automate the deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="c296a-105">Azure에서 Ansible을 사용하여 다른 리소스와 동일한 방식으로 VM(가상 컴퓨터)을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c296a-105">You can use Ansible to manage your virtual machines (VMs) in Azure, the same as you would any other resource.</span></span> <span data-ttu-id="c296a-106">이 문서에서는 Ansible을 사용하여 전체 Linux 환경 및 지원 리소스를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c296a-106">This article shows you how to create a complete Linux environment and supporting resources with Ansible.</span></span> <span data-ttu-id="c296a-107">또한 [Ansible을 사용하여 기본 VM을 만드는](ansible-create-vm.md) 방법을 배울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c296a-107">You can also learn how to [Create a basic VM with Ansible](ansible-create-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="c296a-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c296a-108">Prerequisites</span></span>
<span data-ttu-id="c296a-109">Ansible을 사용하여 Azure 리소스를 관리하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c296a-109">To manage Azure resources with Ansible, you need the following:</span></span>

- <span data-ttu-id="c296a-110">호스트 시스템에 설치된 Ansible 및 Azure Python SDK 모듈</span><span class="sxs-lookup"><span data-stu-id="c296a-110">Ansible and the Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="c296a-111">[Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) 및 [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)에 Ansible 설치</span><span class="sxs-lookup"><span data-stu-id="c296a-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="c296a-112">Azure 자격 증명 및 이를 사용하도록 구성된 Ansible</span><span class="sxs-lookup"><span data-stu-id="c296a-112">Azure credentials, and Ansible configured to use them.</span></span>
    - [<span data-ttu-id="c296a-113">Azure 자격 증명 만들기 및 Ansible 구성</span><span class="sxs-lookup"><span data-stu-id="c296a-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="c296a-114">Azure CLI 버전 2.0.4 이상</span><span class="sxs-lookup"><span data-stu-id="c296a-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="c296a-115">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c296a-115">Run `az --version` to find the version.</span></span> 
    - <span data-ttu-id="c296a-116">업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c296a-116">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="c296a-117">또한 브라우저에서 [Cloud Shell](/azure/cloud-shell/quickstart)을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c296a-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-virtual-network"></a><span data-ttu-id="c296a-118">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="c296a-118">Create virtual network</span></span>
<span data-ttu-id="c296a-119">Ansible Playbook의 다음 섹션에서는 *10.0.0.0/16* 주소 공간에 *myVnet*이라는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c296a-119">The following section in an Ansible playbook creates a virtual network named *myVnet* in the *10.0.0.0/16* address space:</span></span>

```yaml
- name: Create virtual network
  azure_rm_virtualnetwork:
    resource_group: myResourceGroup
    name: myVnet
    address_prefixes: "10.10.0.0/16"
```

<span data-ttu-id="c296a-120">서브넷을 추가하기 위해 다음 섹션에서는 *myVnet* 가상 네트워크에 *mySubnet*이라는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c296a-120">To add a subnet, the following section creates a subnet named *mySubnet* in the *myVnet* virtual network:</span></span>

```yaml
- name: Add subnet
  azure_rm_subnet:
    resource_group: myResourceGroup
    name: mySubnet
    address_prefix: "10.0.1.0/24"
    virtual_network: myVnet
```


## <a name="create-public-ip-address"></a><span data-ttu-id="c296a-121">공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="c296a-121">Create public IP address</span></span>
<span data-ttu-id="c296a-122">인터넷을 통해 리소스에 액세스하려면 공용 IP 주소를 만들어 VM에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="c296a-122">To access resources across the Internet, create and assign a public IP address to your VM.</span></span> <span data-ttu-id="c296a-123">Ansible Playbook의 다음 섹션에서는 *myPublicIP*라는 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c296a-123">The following section in an Ansible playbook creates a public IP address named *myPublicIP*:</span></span>

```yaml
- name: Create public IP address
  azure_rm_publicipaddress:
    resource_group: myResourceGroup
    allocation_method: Static
    name: myPublicIP
```


## <a name="create-network-security-group"></a><span data-ttu-id="c296a-124">네트워크 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="c296a-124">Create Network Security Group</span></span>
<span data-ttu-id="c296a-125">네트워크 보안 그룹은 VM 내/외부 네트워크 트래픽의 흐름을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="c296a-125">Network Security Groups control the flow of network traffic in and out of your VM.</span></span> <span data-ttu-id="c296a-126">Ansible Playbook의 다음 섹션에서는 *myNetworkSecurityGroup*이라는 네트워크 보안 그룹을 만들고 TCP 포트 22에서 SSH 트래픽을 허용하는 규칙을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c296a-126">The following section in an Ansible playbook creates a network security group named *myNetworkSecurityGroup* and defines a rule to allow SSH traffic on TCP port 22:</span></span>

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


## <a name="create-virtual-network-interface-card"></a><span data-ttu-id="c296a-127">가상 네트워크 인터페이스 카드 만들기</span><span class="sxs-lookup"><span data-stu-id="c296a-127">Create virtual network interface card</span></span>
<span data-ttu-id="c296a-128">가상 NIC(네트워크 인터페이스 카드)는 지정된 가상 네트워크, 공용 IP 주소 및 네트워크 보안 그룹에 VM을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c296a-128">A virtual network interface card (NIC) connects your VM to a given virtual network, public IP address, and network security group.</span></span> <span data-ttu-id="c296a-129">Ansible Playbook의 다음 섹션에서는 사용자가 만든 가상 네트워킹 리소스에 연결된 *myNIC*라는 가상 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c296a-129">The following section in an Ansible playbook creates a virtual NIC named *myNIC* connected to the virtual networking resources you have created:</span></span>

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


## <a name="create-virtual-machine"></a><span data-ttu-id="c296a-130">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="c296a-130">Create virtual machine</span></span>
<span data-ttu-id="c296a-131">마지막 단계에서는 VM을 만들고 생성한 모든 리소스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c296a-131">The final step is to create a VM and use all the resources created.</span></span> <span data-ttu-id="c296a-132">Ansible Playbook의 다음 섹션에서는 *myVM*이라는 VM을 만들고 *myNIC*라는 가상 NIC를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c296a-132">The following section in an Ansible playbook creates a VM named *myVM* and attaches the virtual NIC named *myNIC*.</span></span> <span data-ttu-id="c296a-133">다음과 같이 *key_data* 쌍으로 사용자 고유의 공개 키 데이터를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c296a-133">Enter your own public key data in the *key_data* pair as follows:</span></span>

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

## <a name="complete-ansible-playbook"></a><span data-ttu-id="c296a-134">전체 Ansible Playbook</span><span class="sxs-lookup"><span data-stu-id="c296a-134">Complete Ansible playbook</span></span>
<span data-ttu-id="c296a-135">이 모든 섹션을 함께 가져오려면 *azure_create_complete_vm.yml*이라는 Ansible Playbook을 만들고 다음 내용을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c296a-135">To bring all these sections together, create an Ansible playbook named *azure_create_complete_vm.yml* and paste the following contents:</span></span>

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

<span data-ttu-id="c296a-136">Ansible에는 모든 리소스를 배포할 리소스 그룹이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c296a-136">Ansible needs a resource group to deploy all your resources into.</span></span> <span data-ttu-id="c296a-137">[az group create](/cli/azure/vm#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c296a-137">Create a resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="c296a-138">다음 예제에서는 *eastus* 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c296a-138">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="c296a-139">Ansible을 사용하여 전체 VM 환경을 만들려면 다음과 같이 Playbook을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c296a-139">To create the complete VM environment with Ansible, run the playbook as follows:</span></span>

```bash
ansible-playbook azure_create_complete_vm.yml
```

<span data-ttu-id="c296a-140">출력은 VM이 성공적으로 만들어졌음을 보여 주는 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="c296a-140">The output looks similar to the following example that shows the VM has been successfully created:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c296a-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c296a-141">Next steps</span></span>
<span data-ttu-id="c296a-142">이 예제에서는 필요한 가상 네트워킹 리소스를 포함하여 전체 VM 환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c296a-142">This example creates a complete VM environment including the required virtual networking resources.</span></span> <span data-ttu-id="c296a-143">기본 옵션을 사용하여 기존 네트워크 리소스에 VM을 만드는 보다 직접적인 예제는 [VM 만들기](ansible-create-vm.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c296a-143">For a more direct example to create a VM into existing network resources with default options, see [Create a VM](ansible-create-vm.md).</span></span>