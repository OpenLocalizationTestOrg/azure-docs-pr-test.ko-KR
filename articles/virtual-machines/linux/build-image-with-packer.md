---
title: "aaaHow toocreate Packer 사용 하 여 Linux Azure VM 이미지 | Microsoft Docs"
description: "자세한 내용은 방법 toouse Packer toocreate 이미지 Azure에서 Linux 가상 컴퓨터"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: 5990598859e73efac477884bc8de5fd5138bf6e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-linux-virtual-machine-images-in-azure"></a>Azure에서 toouse Packer toocreate Linux 가상 컴퓨터 이미지 하는 방법
Azure의 각 가상 컴퓨터 (VM)는 Linux 배포판 hello 및 운영 체제 버전을 정의 하는 이미지에서 만들어집니다. 이미지는 사전 설치된 응용 프로그램 및 구성을 포함할 수 있습니다. hello Azure 마켓플레이스 가장 일반적인 배포와 응용 프로그램 환경에 대 한 첫 번째 및 제 3 자에 대 한 여러 이미지를 제공 하거나 사용자 고유의 사용자 지정 이미지 맞는 tooyour 요구를 만들 수 있습니다. 이 문서 toouse hello 소스 도구를 열고 하는 방법을 자세히 설명 [Packer](https://www.packer.io/) Azure의 toodefine 및 빌드 사용자 지정 이미지입니다.


## <a name="create-azure-resource-group"></a>Azure 리소스 그룹 만들기
Hello 빌드 프로세스 동안 Packer hello 원본 VM는 것과 같이 임시 Azure 리소스를 만듭니다. 이미지 형식으로 사용 하기 위해 VM의 소스가 되 toocapture, 리소스 그룹을 정의 해야 합니다. hello hello Packer 빌드 프로세스의 출력에에서 저장 됩니다이 리소스 그룹.

[az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다. hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치:

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a>Azure 자격 증명 만들기
Packer는 서비스 사용자를 사용하여 Azure를 인증합니다. Azure 서비스 사용자는 앱, 서비스 및 Packer와 같은 자동화 도구를 사용할 수 있는 보안 ID입니다. 제어 하 고이 정보를 toowhat 작업 hello 서비스 사용자는 Azure에서 수행할 수 있는 대로 hello 사용 권한을 정의 합니다.

서비스와 사용자 만들기 [az ad sp 만들기에 대 한-rbac](/cli/azure/ad/sp#create-for-rbac) Packer 해야 하는 출력 hello 자격 증명:

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

Hello 명령 앞에서 hello 출력의 예는 다음과 같습니다.

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

tooauthenticate tooAzure 하면 Azure 구독 ID와 tooobtain [az 계정 표시](/cli/azure/account#show):

```azurecli
az account show --query [id] --output tsv
```

Hello 다음 단계에서이 두 명령은에서 hello 출력을 사용합니다.


## <a name="define-packer-template"></a>Packer 템플릿 정의
toobuild 이미지를 JSON 파일로 템플릿을 만듭니다. Hello 서식 파일에 빌더를 정의 하 고 provisioners hello 실제을 수행 하는 빌드 프로세스입니다. Packer에는 [provisioner Azure에 대 한](https://www.packer.io/docs/builders/azure.html) toodefine Azure 사용할 수 있는 hello 서비스 사용자 자격 증명 hello 앞 단계에서에서 만든 등의 리소스입니다.

라는 파일을 만들어 *ubuntu.json* 붙여넣기 hello에 따라 콘텐츠입니다. Hello 다음에 대 한 고유한 값을 입력 합니다.

| 매개 변수                           | 여기서 tooobtain |
|-------------------------------------|----------------------------------------------------|
| *client_id*                         | `az ad sp` create 명령의 첫 번째 출력 줄 - *appId* |
| *client_secret*                     | `az ad sp` create 명령의 두 번째 출력 줄 - *password* |
| *tenant_id*                         | `az ad sp` create 명령의 세 번째 출력 줄 - *tenant* |
| *subscription_id*                   | `az account show` 명령의 출력 |
| *managed_image_resource_group_name* | Hello 첫 번째 단계에서 만든 리소스 그룹의 이름 |
| *managed_image_name*                | 만들어진 hello 관리 되는 디스크 이미지에 대 한 이름 |


```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
    "client_secret": "0e760437-bf34-4aad-9f8d-870be799c55d",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Linux",
    "image_publisher": "Canonical",
    "image_offer": "UbuntuServer",
    "image_sku": "16.04-LTS",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "execute_command": "chmod +x {{ .Path }}; {{ .Vars }} sudo -E sh '{{ .Path }}'",
    "inline": [
      "apt-get update",
      "apt-get upgrade -y",
      "apt-get -y install nginx",

      "/usr/sbin/waagent -force -deprovision+user && export HISTSIZE=0 && sync"
    ],
    "inline_shebang": "/bin/sh -x",
    "type": "shell"
  }]
}
```

이 서식 파일 16.04 Ubuntu LTS 이미지 NGINX, 설치를 다음 hello VM deprovisions 합니다.

> [!NOTE]
> 이 서식 파일 tooprovision 사용자 자격 증명 확장 하는 경우 조정 deprovisions hello Azure 에이전트 tooread는 hello provisioner 명령 `-deprovision` 대신 `deprovision+user`합니다.
> hello `+user` 플래그 hello 원본 VM에서에서 모든 사용자 계정을 제거 합니다.


## <a name="build-packer-image"></a>Packer 이미지 작성
로컬 컴퓨터에 설치 된 Packer 아직 없는 경우 [hello Packer 설치 지침을 따라](https://www.packer.io/docs/install/index.html)합니다.

Hello 이미지 프로그램 Packer를 지정 하 여 서식 파일을 다음과 같이 만듭니다.

```bash
./packer build ubuntu.json
```

Hello 명령 앞에서 hello 출력의 예는 다음과 같습니다.

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> dept : Engineering
==> azure-arm:  ->> task : Image deployment
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.218.147’
==> azure-arm: Waiting for SSH toobecome available...
==> azure-arm: Connected tooSSH!
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-shell868574263
    azure-arm: WARNING! hello waagent service will be stopped.
    azure-arm: WARNING! Cached DHCP leases will be deleted.
    azure-arm: WARNING! root password will be disabled. You will not be able toologin as root.
    azure-arm: WARNING! /etc/resolvconf/resolv.conf.d/tail and /etc/resolvconf/resolv.conf.d/original will be deleted.
    azure-arm: WARNING! packer account and entire home directory will be deleted.
==> azure-arm: Querying hello machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-swtxmqm7ly/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Compute Name              : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```


## <a name="create-vm-from-azure-image"></a>Azure 이미지에서 VM 만들기
이제 [az vm create](/cli/azure/vm#create)를 사용하여 이미지에서 VM을 만들 수 있습니다. Hello hello를 사용 하 여 만든 이미지를 지정 `--image` 매개 변수입니다. hello 다음 예제에서는 V *myVM* 에서 *myPackerImage* 이미 존재 하지 않는 경우 SSH 키를 생성 합니다.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

몇 분 toocreate hello VM이 필요합니다. Hello VM을 만든 후 기록해 hello `publicIpAddress` hello Azure CLI로 표시 합니다. 이 주소는 웹 브라우저를 통해 사용 되는 tooaccess hello NGINX 사이트입니다.

tooallow 웹 트래픽 tooreach VM을 열고에 포트 80에서 인터넷 hello [az vm-포트를 열](/cli/azure/vm#open-port):

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a>VM 및 NGINX 테스트
웹 브라우저를 열고 입력 수 이제 `http://publicIpAddress` hello 주소 표시줄에 있습니다. 제공 하려면 사용자 고유의 공용 hello VM의에서 IP 주소를 만드는 프로세스입니다. 다음 예제는 hello와 같이 hello 기본 NGINX 페이지가 표시 됩니다.

![NGINX 기본 사이트](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a>다음 단계
이 예제에서는 이미 설치 되어 NGINX Packer toocreate VM 이미지를 사용한 것입니다. 이 VM 이미지 toodeploy 앱 tooVMs hello Ansible, Chef 또는 Puppet를 사용 하 여 이미지에서에서 만든 같은 기존 배포 워크플로 함께 사용할 수 있습니다.

다른 Linux 배포판에 대한 추가 예제 Packer 템플릿은 [이 GitHub 리포지토리](https://github.com/hashicorp/packer/tree/master/examples/azure)를 참조하세요.