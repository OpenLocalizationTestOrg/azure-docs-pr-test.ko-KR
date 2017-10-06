---
title: "Linux VM aaaUse 클라우드 init toocustomize | Microsoft Docs"
description: "가 Linux VM a toouse 클라우드 init toocustomize Azure CLI 2.0 hello 하는 방법"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 195c22cd-4629-4582-9ee3-9749493f1d72
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e7297e162fc73f0da42f195bec2fcbe23b310c1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation"></a>클라우드 init toocustomize Linux VM을 만드는 동안 사용
이 문서에서는 방법 toomake 클라우드 초기화 스크립트 tooset hello 호스트 이름, 설치 된 패키지를 업데이트 및 Azure CLI 2.0 hello로 사용자 계정을 관리 합니다. hello 클라우드 초기화 스크립트는 Azure CLI에서 가상 컴퓨터 (VM)를 만들 때 호출 됩니다. 응용 프로그램 설치, 구성 파일 작성 및 Key Vault의 키 삽입에 대한 보다 깊이 있는 개요를 보려면 [이 자습서](tutorial-automate-vm-deployment.md)를 참조하세요. Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](using-cloud-init-nodejs.md)합니다.

## <a name="quick-commands"></a>빠른 명령
Hello 호스트 이름을 설정 하는 모든 패키지를 업데이트 하 고 sudo 사용자 tooLinux를 추가 하는 클라우드 init.txt 스크립트를 만듭니다.

```yaml
#cloud-config
hostname: myVMhostname
apt_upgrade: true
users:
  - name: myNewAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myVM
```

리소스 그룹 toolaunch에 Vm을 만들 [az 그룹 만들기](/cli/azure/group#create)합니다. hello 다음 예제에서는 명명 된 hello 리소스 그룹 *myResourceGroup*:

```azurecli
az group create --name myResourceGroup --location eastus
```

사용 하 여 Linux VM을 만들 [az vm 만들기](/cli/azure/vm#create) 클라우드 init tooconfigure를 사용 하 여 hello로 부팅 하는 동안 그 `--custom-data` 매개 변수입니다.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a>자세한 연습
새 Linux VM을 시작하면 사용자 지정된 사항이나 사용자의 요구에 맞게 준비된 기능이 없는 표준 Linux VM이 시작됩니다. [클라우드 init](https://cloudinit.readthedocs.org) 는 표준 방법 tooinject는 스크립트 또는 구성 설정을 해당 Linux VM에 처음으로 hello에 대해 부팅 합니다.

Azure에서 몇 가지 여러 가지 Linux VM에 toomake 변경 중인 배포 되거나 부팅 합니다.

* cloud-init을 사용하여 스크립트를 삽입합니다.
* Azure hello를 사용 하 여 스크립트 삽입 [VMAccess 확장](using-vmaccess-extension.md)합니다.
* Azure 템플릿을 사용합니다(cloud-init 사용).
* Azure 템플릿을 사용합니다( [CustomScriptExtention](extensions-customscript.md)사용).

부팅 후 언제 든 지 tooinject 스크립트:

* SSH toorun 명령을 직접
* Azure hello를 사용 하 여 스크립트 삽입 [VMAccess 확장](using-vmaccess-extension.md), 명령적으로 또는 Azure 서식 파일
* Ansible, Salt, Chef, Puppet 등의 구성 관리 도구를 사용합니다.

> [!NOTE]
> VMAccess 확장 hello 동일한 루트 대로 스크립트를 실행 합니다. SSH를 사용 하 여 수 있습니다. 그러나 hello VM 확장을 사용 하 여 사용 하면 몇 가지 기능 시나리오에 따라 유용할 수 있는 Azure 제공 하 합니다.

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a>Azure VM 빨리 만들기 이미지 별칭에 대한 cloud-init 사용 가능 여부
| Alias | 게시자 | 제안 | SKU | 버전 | cloud-init |
|:--- |:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |Centos |7.2 |최신 |no |
| CoreOS |CoreOS |CoreOS |Stable |최신 |yes |
| Debian |credativ |Debian |8 |최신 |no |
| openSUSE |SUSE |openSUSE |13.2 |최신 |no |
| RHEL |Redhat |RHEL |7.2 |최신 |no |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |최신 |yes |

TooAzure를 제공 하는 hello 이미지에서 작업 및 우리의 파트너 tooget 클라우드 초기화 포함을 사용 하는입니다.

## <a name="add-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a>추가 Azure CLI hello에 대 한 클라우드 초기화 스크립트 toohello VM 만들기
hello Azure CLI를 사용 하 여 hello 클라우드 초기화 파일을 지정 하는 azure에서 VM을 만들 때 클라우드 초기화 스크립트 toolaunch `--custom-data` 전환 합니다.

리소스 그룹 toolaunch에 Vm을 만들 [az 그룹 만들기](/cli/azure/group#create)합니다. hello 다음 예제에서는 명명 된 hello 리소스 그룹 *myResourceGroup*:

```azurecli
az group create --name myResourceGroup --location eastus
```

사용 하 여 Linux VM을 만들 [az vm 만들기](/cli/azure/vm#create) 클라우드 init tooconfigure를 사용 하 여 부팅 하는 동안 것입니다.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a>Linux VM의 클라우드 초기화 스크립트 tooset hello 호스트 만들기
가장 간단한 hello 및 모든 Linux VM에 대 한 가장 중요 한 설정 중 하나를 hello hostname 것입니다. 이 스크립트와 함께 cloud-init을 사용하여 손쉽게 설정할 수 있습니다.  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a>예제 cloud-init 스크립트 `cloud_config_hostname.txt`
```yaml
#cloud-config
hostname: myservername
```

이 클라우드 초기화 스크립트의 hello VM hello 초기 시작 하는 동안 hello hostname 너무 설정*myservername*합니다. 사용 하 여 Linux VM을 만들 [az vm 만들기](/cli/azure/vm#create) 클라우드 init tooconfigure를 사용 하 여 부팅 하는 동안 것입니다.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

로그인의 hello hello 호스트 이름 확인 및 새 VM입니다.

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a>cloud-init 스크립트 만들기
보안을 위해 hello 처음 부팅할 때 Ubuntu VM tooupdate 프로그램 할 수 있습니다. 클라우드 초기화를 사용 하 여 hello로 따르는지 스크립트를 사용 하는 hello Linux 배포에 따라 수행할 수 있습니다.

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a>다음 스크립트 예에서는 클라우드 init `cloud_config_apt_upgrade.txt` hello Debian 제품군에 대 한
```yaml
#cloud-config
apt_upgrade: true
```

통해 모든 hello 설치 패키지는 업데이트 Linux 부팅 된 후 **apt get**합니다. 사용 하 여 Linux VM을 만들 [az vm 만들기](/cli/azure/vm#create) 클라우드 init tooconfigure를 사용 하 여 부팅 하는 동안 것입니다.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

로그인한 다음 모든 패키지가 업데이트되었는지 확인합니다.

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
hello following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 tooremove and 0 not upgraded.
```

## <a name="create-a-cloud-init-script-tooadd-a-user-toolinux"></a>클라우드 초기화 스크립트 tooadd 사용자 tooLinux 만들기
모든 새로운 Linux VM에 있는 hello 첫 번째 작업 중 하나는 tooadd 자신이 나 tooavoid 사용에 대 한 사용자 *루트*합니다. SSH 키가 유용성 및 보안에 대 한 모범 사례 및 toohello 추가 될 *~/.ssh/authorized_keys* 이 클라우드 초기화 스크립트 파일입니다.

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a>Debian 제품군용 예제 cloud-init 스크립트 `cloud_config_add_users.txt`
```yaml
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

Linux 부팅 된 후에 모든 나열 된 hello 사용자는 생성 되 고 추가 된 toohello sudo 그룹. 사용 하 여 Linux VM을 만들 [az vm 만들기](/cli/azure/vm#create) 클라우드 init tooconfigure를 사용 하 여 부팅 하는 동안 것입니다.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

로그인 하 고 hello 새로 만든 사용자를 확인 합니다.

```bash
ssh myVM
cat /etc/group
```

출력

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a>다음 단계
클라우드 init은 되 고 하나의 표준 방식으로 toomodify Linux VM에서 부팅 합니다. Azure에 toomodify 수 있게 해 주는 VM 확장 프로그램 LinuxVM 부팅 또는 실행 되는 동안 있습니다. 예를 들어 hello VM에서 실행 되는 동안 hello Azure VMAccessExtension tooreset SSH 또는 사용자 정보 사용할 수 있습니다. 클라우드-init로 tooreset hello 암호를 다시 부팅 해야 합니다.

[가상 컴퓨터 확장 및 기능 정보](extensions-features.md)

[사용자, SSH, 및 확인 또는 복구 디스크를 사용 하 여 Azure Linux Vm에서 VMAccess 확장을 환영](using-vmaccess-extension.md)
