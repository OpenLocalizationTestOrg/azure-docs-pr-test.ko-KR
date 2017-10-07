---
title: "aaaInstall 및 Azure 가상 컴퓨터를 사용 하기 위해 Ansible 구성 | Microsoft Docs"
description: "자세한 내용은 방법 tooinstall Ansible Ubuntu, CentOS 및 SLES에서 Azure 리소스를 관리 하기 위한 구성"
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
ms.openlocfilehash: b33d1893909b6134a5474617c9af2d6e4f627c05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-ansible-toomanage-virtual-machines-in-azure"></a>설치 하 고 Azure에서 Ansible toomanage 가상 컴퓨터 구성
이 문서 tooinstall Ansible와 필수 Azure Python SDK 모듈의 일부에 대 한 가장 일반적인 Linux 배포판 hello 방법을 자세히 설명 합니다. 에 설치할 수 있습니다 Ansible 다른 배포판 hello 설치 패키지 toofit 조정 하 여 특정 플랫폼에 있습니다. toocreate Azure 안전한 방식으로 리소스를 배울 있습니다 어떻게 toocreate Ansible toouse에 대 한 자격 증명을 정의 합니다. 

자세한 설치 옵션 및 다른 플랫폼에 대 한 단계에 대 한 참조 hello [Ansible 설치 가이드](https://docs.ansible.com/ansible/intro_installation.html)합니다.


## <a name="install-ansible"></a>Ansible 설치
먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다. hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroupAnsible* hello에 *eastus* 위치:

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

이제 VM을 만들고 Ansible hello 배포판을 다음 중 하나에 대 한 설치:

- [Ubuntu 16.04 LTS](#ubuntu1604-lts)
- [CentOS 7.3](#centos-73)
- [SLES 12.2 SP2](#sles-122-sp2)

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS
[az vm create](/cli/azure/vm#create)로 VM을 만듭니다. hello 다음 예제에서는 V *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour VM를 사용 하 여 hello `publicIpAddress` hello에 명시 된 hello VM에서에서 출력 만들기 작업:

```bash
ssh azureuser@<publicIpAddress>
```

VM에 Azure Python SDK 모듈과 Ansible hello에 대 한 hello 필요한 패키지를 다음과 같이 설치 합니다.

```bash
## Install pre-requisite packages
sudo apt-get update && sudo apt-get install -y libssl-dev libffi-dev python-dev python-pip

## Install Azure SDKs via pip
pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via apt
sudo apt-get install -y software-properties-common
sudo apt-add-repository -y ppa:ansible/ansible
sudo apt-get update && sudo apt-get install -y ansible
```

이제 너무 이동[만들 Azure 자격 증명](#create-azure-credentials)합니다.


### <a name="centos-73"></a>CentOS 7.3
[az vm create](/cli/azure/vm#create)로 VM을 만듭니다. hello 다음 예제에서는 V *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour VM를 사용 하 여 hello `publicIpAddress` hello에 명시 된 hello VM에서에서 출력 만들기 작업:

```bash
ssh azureuser@<publicIpAddress>
```

VM에 Azure Python SDK 모듈과 Ansible hello에 대 한 hello 필요한 패키지를 다음과 같이 설치 합니다.

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Azure SDKs via pip
sudo pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via yum
sudo yum install -y ansible
```

이제 너무 이동[만들 Azure 자격 증명](#create-azure-credentials)합니다.


### <a name="sles-122-sp2"></a>SLES 12.2 SP2
[az vm create](/cli/azure/vm#create)로 VM을 만듭니다. hello 다음 예제에서는 V *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour VM를 사용 하 여 hello `publicIpAddress` hello에 명시 된 hello VM에서에서 출력 만들기 작업:

```bash
ssh azureuser@<publicIpAddress>
```

VM에 Azure Python SDK 모듈과 Ansible hello에 대 한 hello 필요한 패키지를 다음과 같이 설치 합니다.

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 python-devel \
    libopenssl-devel python-pip python-setuptools python-azure-sdk

## Install Ansible via zypper
sudo zypper addrepo http://download.opensuse.org/repositories/systemsmanagement/SLE_12_SP2/systemsmanagement.repo
sudo zypper refresh && sudo zypper install ansible
```

이제 너무 이동[만들 Azure 자격 증명](#create-azure-credentials)합니다.


## <a name="create-azure-credentials"></a>Azure 자격 증명 만들기
Ansible은 사용자 이름 및 암호 또는 서비스 주체를 사용하여 Azure와 통신합니다. Azure 서비스 주체는 앱, 서비스 및 Ansible과 같은 자동화 도구를 사용할 수 있는 보안 ID입니다. 제어 하 고이 정보를 toowhat 작업 hello 서비스 사용자는 Azure에서 수행할 수 있는 대로 hello 사용 권한을 정의 합니다. 제공 하는 것 사용자 이름 및 암호를 통해 tooimprove 보안,이 예제에서는 기본 서비스 보안 주체

서비스와 사용자 만들기 [az ad sp 만들기에 대 한-rbac](/cli/azure/ad/sp#create-for-rbac) Ansible 해야 하는 출력 hello 자격 증명:

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

Hello 명령 앞에서 hello 출력의 예는 다음과 같습니다.

```json
[
  "eec5624a-90f8-4386-8a87-02730b5410d5",
  "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "72f988bf-86f1-41af-91ab-2d7cd011db47"
]
```

tooauthenticate tooAzure 하면 Azure 구독 ID와 tooobtain [az 계정 표시](/cli/azure/account#show):

```azurecli
az account show --query [id] --output tsv
```

Hello 다음 단계에서이 두 명령은에서 hello 출력을 사용합니다.


## <a name="create-ansible-credentials-file"></a>Ansible 자격 증명 파일 만들기
tooprovide tooAnsible 자격 증명을 환경 변수를 정의 하거나 로컬 자격 증명 파일을 만듭니다. 방법에 대 한 자세한 내용은 toodefine Ansible 자격 증명 참조 [자격 증명을 제공 하 tooAzure 모듈](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules)합니다. 

개발 환경의 경우 호스트 VM에서 다음과 같이 Ansible에 대한 *자격 증명* 파일을 만듭니다.

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

hello *자격 증명* 파일 자체 hello 구독 ID를 결합 하 여 서비스 사용자를 만드는 hello 출력을 제공 합니다. 이전 hello에서 출력 [az ad sp 만들기에 대 한-rbac](/cli/azure/ad/sp#create-for-rbac) 동일 hello 명령입니다 필요에 따라 주문 *client_id*, *비밀*, 및 *테 넌 트* . 다음 예에서는 hello *자격 증명* 파일 hello 이전 출력 일치 하는 이러한 값을 보여 줍니다. 다음과 같이 사용자 고유의 값을 입력합니다.

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
secret=b8326643-f7e9-48fb-b0d5-952b68ab3def
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a>Ansible 환경 변수 사용
Toouse Ansible 타워 또는 Jenkins 등의 도구를 사용 하도록 하려는 경우 환경 변수를 다음과 같이 정의할 수 있습니다. 이러한 변수 서비스 보안 주체를 만드는 hello 출력 hello 구독 ID를 결합 합니다. 이전 hello에서 출력 [az ad sp 만들기에 대 한-rbac](/cli/azure/ad/sp#create-for-rbac) 명령 동일 hello입니다 필요에 따라 주문 *AZURE_CLIENT_ID*, *AZURE_SECRET*, 및 *AZURE_ 테 넌 트*합니다. 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
export AZURE_SECRET=8326643-f7e9-48fb-b0d5-952b68ab3def
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a>다음 단계
Ansible 있으며 Azure Python SDK 모듈 설치 및 자격 증명 Ansible toouse에 대해 정의 된 hello 필요한 수 있습니다. 너무 방법에 대해 알아봅니다[VM Ansible을 만들어](ansible-create-vm.md)합니다. 배울 수 있습니다 어떻게 너무[전체 Azure VM을 만들고 Ansible 사용 하 여 리소스를 지 원하는](ansible-create-complete-vm.md)합니다.
