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
# <a name="create-a-complete-linux-virtual-machine-environment-in-azure-with-ansible"></a>Azure에서 Ansible을 사용하여 전체 Linux 가상 컴퓨터 환경 만들기
Ansible 있습니다 tooautomate hello 배포 및 구성 리소스의 사용자 환경에서. Azure에서 가상 컴퓨터 (Vm) Ansible toomanage을 사용 하 여, 다른 리소스와 마찬가지로 동일한 hello 수 있습니다. 이 문서에서는 어떻게 toocreate 완벽 한 Linux 환경 및 Ansible 사용 하 여 리소스를 지원 합니다. 배울 수 있습니다 어떻게 너무[Ansible 기본 VM 만들기](ansible-create-vm.md)합니다.


## <a name="prerequisites"></a>필수 조건
Azure toomanage Ansible 사용 하 여 리소스를 해야 다음 hello:

- Ansible 호스트 시스템에 설치 된 Azure Python SDK 모듈 hello 및 합니다.
    - [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) 및 [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)에 Ansible 설치
- Azure 자격 증명 및 구성 Ansible toouse 해당 합니다.
    - [Azure 자격 증명 만들기 및 Ansible 구성](ansible-install-configure.md#create-azure-credentials)
- Azure CLI 버전 2.0.4 이상 실행 `az --version` toofind hello 버전입니다. 
    - Tooupgrade 필요한 경우 참조 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 또한 브라우저에서 [Cloud Shell](/azure/cloud-shell/quickstart)을 사용할 수도 있습니다.


## <a name="create-virtual-network"></a>가상 네트워크 만들기
hello는 Ansible 플레이 북의 다음 섹션 가상 네트워크를 만들어 명명 된 *myVnet* hello에 *10.0.0.0/16* 주소 공간:

```yaml
- name: Create virtual network
  azure_rm_virtualnetwork:
    resource_group: myResourceGroup
    name: myVnet
    address_prefixes: "10.10.0.0/16"
```

서브넷 tooadd 다음 단원을 hello 이라는 서브넷을 만듭니다. *mySubnet* hello에 *myVnet* 가상 네트워크:

```yaml
- name: Add subnet
  azure_rm_subnet:
    resource_group: myResourceGroup
    name: mySubnet
    address_prefix: "10.0.1.0/24"
    virtual_network: myVnet
```


## <a name="create-public-ip-address"></a>공용 IP 주소 만들기
hello 인터넷을 통해 tooaccess 리소스 만들고 공용 IP 주소 tooyour VM을 할당 합니다. hello는 Ansible 플레이 북의 다음 섹션 공용 IP 주소를 만들고 명명 된 *myPublicIP*:

```yaml
- name: Create public IP address
  azure_rm_publicipaddress:
    resource_group: myResourceGroup
    allocation_method: Static
    name: myPublicIP
```


## <a name="create-network-security-group"></a>네트워크 보안 그룹 만들기
네트워크 보안 그룹 VM 내부 및 외부 네트워크 트래픽의 hello 흐름을 제어 합니다. hello 다음 섹션에는 Ansible 플레이 북 네트워크 보안 그룹을 만듭니다 라는 *myNetworkSecurityGroup* 하 고 TCP 포트 22에서 규칙 tooallow SSH 트래픽 정의:

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


## <a name="create-virtual-network-interface-card"></a>가상 네트워크 인터페이스 카드 만들기
가상 네트워크 인터페이스 카드 (NIC) 가상 네트워크, 공용 IP 주소 및 네트워크 보안 그룹을 지정 하 여 VM tooa를 연결 합니다. hello는 Ansible 플레이 북의 다음 섹션을 만듭니다 라는 가상 NIC *myNIC* 만든 toohello 가상 네트워킹 리소스를 연결 합니다.

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


## <a name="create-virtual-machine"></a>가상 컴퓨터 만들기
hello 마지막 단계가 toocreate VM 및 생성 된 모든 hello 리소스를 사용 합니다. hello는 Ansible 플레이 북의 다음 섹션을 만듭니다 라는 VM *myVM* 연결 합니다. 명명 된 가상 NIC hello 및 *myNIC*합니다. Hello에 공용 키 데이터를 입력 *key_data* 다음과 같이 쌍으로 연결 합니다.

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

## <a name="complete-ansible-playbook"></a>전체 Ansible Playbook
toobring 만들 라는 Ansible 플레이 북 함께이 섹션에서는 모든 *azure_create_complete_vm.yml* 붙여넣기 hello 내용에 따라:

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

Ansible에 모든 리소스를 리소스 그룹 toodeploy 필요합니다. [az group create](/cli/azure/vm#create)를 사용하여 리소스 그룹을 만듭니다. hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치:

```azurecli
az group create --name myResourceGroup --location eastus
```

toocreate hello 완료 VM 환경과 Ansible, hello 플레이 북을 다음과 같이 실행:

```bash
ansible-playbook azure_create_complete_vm.yml
```

hello 출력은 다음 VM 성공적으로 만들었습니다. hello를 보여 주는 예제와 비슷한 toohello 합니다.

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

## <a name="next-steps"></a>다음 단계
이 예제에는 필요한 hello 가상 네트워킹 리소스를 포함 하 여 완벽 한 VM 환경을 만듭니다. 직접적 예제 toocreate 기본 옵션으로 기존 네트워크 리소스에 VM 참조 하십시오. [VM을 만들](ansible-create-vm.md)합니다.
