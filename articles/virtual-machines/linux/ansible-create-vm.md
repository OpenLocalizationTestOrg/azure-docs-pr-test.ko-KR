---
title: "Azure에서 기본 Linux VM aaaUse Ansible toocreate | Microsoft Docs"
description: "자세한 내용은 방법 toouse Ansible toocreate 기본 Azure에서 Linux 가상 컴퓨터를 관리 하 고"
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
ms.openlocfilehash: ffe278b3f846924ff9c4d026120565146f951152
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a>Azure에서 Ansible을 사용하여 기본 가상 컴퓨터 만들기
Ansible 있습니다 tooautomate hello 배포 및 구성 리소스의 사용자 환경에서. Azure에서 가상 컴퓨터 (Vm) Ansible toomanage을 사용 하 여, 다른 리소스와 마찬가지로 동일한 hello 수 있습니다. 이 문서에서는 어떻게 toocreate Ansible 사용 하 여 기본 VM입니다. 배울 수 있습니다 어떻게 너무[Ansible 완벽 한 VM 환경을 만들기](ansible-create-complete-vm.md)합니다.


## <a name="prerequisites"></a>필수 조건
Azure toomanage Ansible 사용 하 여 리소스를 해야 다음 hello:

- Ansible 호스트 시스템에 설치 된 Azure Python SDK 모듈 hello 및 합니다.
    - [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) 및 [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)에 Ansible 설치
- Azure 자격 증명 및 구성 Ansible toouse 해당 합니다.
    - [Azure 자격 증명 만들기 및 Ansible 구성](ansible-install-configure.md#create-azure-credentials)
- Azure CLI 버전 2.0.4 이상 실행 `az --version` toofind hello 버전입니다. 
    - Tooupgrade 필요한 경우 참조 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 또한 브라우저에서 [Cloud Shell](/azure/cloud-shell/quickstart)을 사용할 수도 있습니다.


## <a name="create-supporting-azure-resources"></a>지원 Azure 리소스 만들기
이 예제에서는 기존 인프라에 VM을 배포하는 runbook을 만듭니다. 먼저 [az group create](/cli/azure/vm#create)를 사용하여 리소스 그룹을 만듭니다. hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치:

```azurecli
az group create --name myResourceGroup --location eastus
```

[az network vnet create](/cli/azure/network/vnet#create)를 사용하여 VM의 가상 네트워크를 만듭니다. hello 다음 예제에서는 가상 네트워크를 만들어 명명 된 *myVnet* 및 명명 된 서브넷 *mySubnet*:

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a>Ansible Playbook 만들기 및 실행
명명 된 프로그램 Ansible 플레이 북 만들기 **azure_create_vm.yml** 붙여넣기 hello 내용에 따라 합니다. 이 예제에서는 단일 VM을 만들고 SSH 자격 증명을 구성합니다. Hello에 공용 키 데이터를 입력 *key_data* 다음과 같이 쌍으로 연결 합니다.

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

toocreate hello hello 플레이 북을 다음과 같이 실행 Ansible의 VM:

```bash
ansible-playbook azure_create_vm.yml
```

hello 출력은 다음 VM 성공적으로 만들었습니다. hello를 보여 주는 예제와 비슷한 toohello 합니다.

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a>다음 단계
이 예제에서는 기존 리소스 그룹에 VM을 만들고 이미 배포된 가상 네트워크를 사용합니다. 자세한 예는 방법에 대 한 가상 네트워크 및 네트워크 보안 그룹 규칙 같은 toouse Ansible toocreate 지원 리소스 참조 [Ansible 완벽 한 VM 환경을 만들기](ansible-create-complete-vm.md)합니다.
