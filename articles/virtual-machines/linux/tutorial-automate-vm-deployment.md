---
title: "Linux VM에 Azure에서 처음 부팅 aaaCustomize | Microsoft Docs"
description: "어떻게 toouse 클라우드 init 및 주요 자격 증명 모음 toocustomze Linux Vm의 경우 hello 처음 부팅 될 Azure에 알아봅니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 280189723ac0205226f9c0068bd605da13249ace
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-linux-virtual-machine-on-first-boot"></a>어떻게 toocustomize 첫 번째 부팅의 Linux 가상 컴퓨터
이전 자습서에서는 방법에 대해 배웠습니다 tooSSH tooa 가상 컴퓨터 (VM) NGINX를 수동으로 설치 합니다. Vm을 신속 하 고 일관 된 방식으로 자동화 toocreate 방법이 일반적으로 필요 합니다. 일반적인 접근 방식을 toocustomize 첫 번째 부팅 시 VM은 toouse [클라우드 init](https://cloudinit.readthedocs.io)합니다. 이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * cloud-init 구성 파일 만들기
> * cloud-init 파일을 사용하는 VM 만들기
> * VM이 생성 하는 hello 후 실행 중인 Node.js 응용 프로그램 보기
> * 주요 자격 증명 모음 toosecurely 인증서 저장소를 사용 하 여
> * cloud-init를 사용하여 NGINX 배포 자동화


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.  



## <a name="cloud-init-overview"></a>Cloud-init 개요
[클라우드 init](https://cloudinit.readthedocs.io) 는 널리 사용 되는 접근 방식을 toocustomize Linux VM 처음으로 hello에 대 한 부팅 합니다. 클라우드 init tooinstall 패키지를 사용할 수 있으며 파일, 또는 tooconfigure 사용자 및 보안에 기록할 수 있습니다. 추가 단계 없이 없는 클라우드 init hello 초기 부팅 프로세스 중 실행 될 때 또는 에이전트 tooapply 구성에 필요 합니다.

Cloud-init는 배포에서도 작동합니다. 예를 들어 사용 하지 않는 **apt get 설치** 또는 **yum 설치** tooinstall 패키지 합니다. 대신 패키지 tooinstall의 목록을 정의할 수 있습니다. 클라우드 init 자동으로 선택 하는 hello 배포판에 대 한 hello 네이티브 패키지 관리 도구를 사용 합니다.

TooAzure를 제공 하는 hello 이미지에서 작업 및 우리의 파트너 tooget 클라우드 초기화 포함을 사용 하는입니다. 다음 표에서 hello Azure 플랫폼 이미지에 현재 클라우드 init 가용성 hello를 설명 합니다.

| Alias | 게시자 | 제안 | SKU | 버전 |
|:--- |:--- |:--- |:--- |:--- |:--- |
| UbuntuLTS |Canonical |UbuntuServer |16.04-LTS |최신 |
| UbuntuLTS |Canonical |UbuntuServer |14.04.5-LTS |최신 |
| CoreOS |CoreOS |CoreOS |Stable |최신 |


## <a name="create-cloud-init-config-file"></a>cloud-init 구성 파일 만들기
toosee 클라우드 초기화 작업에서 NGINX를 설치 하 고 간단한 ' Hello World' Node.js 응용 프로그램을 실행 하는 VM을 만듭니다. 같은 클라우드 init 구성이 hello hello 필요한 패키지를 설치, Node.js 응용 프로그램을 만들고 초기화 하 고 hello 앱이 시작 됩니다.

현재 셸에서 라는 파일을 만들어 *클라우드 init.txt* 붙여넣기 hello 구성에 따라 합니다. 예를 들어 로컬 컴퓨터에 없는 클라우드 셸 hello에 hello 파일을 만듭니다. 원하는 모든 편집기를 사용할 수 있습니다. 입력 `sensible-editor cloud-init.txt` toocreate 파일 hello 및 사용할 수 있는 편집기의 목록을 확인 합니다. 해당 hello 전체 클라우드 init 파일을 올바르게 복사 했는지 확인, 특히 첫 번째 줄을 hello:

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

cloud-init 구성 옵션에 대한 자세한 내용은 [cloud-init 구성 예제](https://cloudinit.readthedocs.io/en/latest/topics/examples.html)를 참조하세요.

## <a name="create-virtual-machine"></a>가상 컴퓨터 만들기
VM을 만들려면 먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다. hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroupAutomate* hello에 *eastus* 위치:

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

이제 [az vm create](/cli/azure/vm#create)로 VM을 만듭니다. 사용 하 여 hello `--custom-data` 클라우드 init 구성 파일에서 매개 변수 toopass 합니다. Hello 전체 경로 toohello 제공 *클라우드 init.txt* config 현재 작업 디렉터리 외부의 hello 파일을 저장 합니다. hello 다음 예제에서는 V *myAutomatedVM*:

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

Hello VM toobe 생성에 대 일 분 정도 걸리며 hello 패키지 tooinstall 및 hello 앱 toostart 합니다. Hello Azure CLI toohello 프롬프트 반환 된 후 toorun 계속 하는 백그라운드 작업 있습니다. 다른 몇 분 hello 앱에 액세스 하려면 먼저 수도 있습니다. Hello VM을 만들면 기록해 hello `publicIpAddress` hello Azure CLI로 표시 합니다. 이 주소는 웹 브라우저를 통해 사용 되는 tooaccess hello Node.js 응용 프로그램입니다.

tooallow 웹 트래픽 tooreach VM을 열고에 포트 80에서 인터넷 hello [az vm-포트를 열](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a>Web App 테스트
웹 브라우저를 열고 입력 수 이제 *http://<publicIpAddress>*  hello 주소 표시줄에 있습니다. 제공 하려면 사용자 고유의 공용 hello VM의에서 IP 주소를 만드는 프로세스입니다. Node.js 앱 hello 다음 예제와 같이 표시 됩니다.

![실행 중인 NGINX 사이트 보기](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a>Key Vault의 인증서 삽입
이 선택적 섹션이 안전 하 게 Azure 키 자격 증명 모음에 인증서를 저장 하는 방법을 hello VM 배포 하는 동안 이러한 구성 요소를 보여 줍니다. Hello 인증서를 포함 하는 사용자 지정 이미지를 사용 하는 대신 구운 기능,이 과정을 사용 하면 가장 최신 인증서 hello은 첫 번째 부팅 시 tooa VM을 삽입 합니다. Hello 과정에서 hello 인증서 되지 hello Azure 플랫폼 벗어나거나 스크립트, 명령줄 기록 또는 서식 파일에 노출 됩니다.

Azure Key Vault는 암호화 키 및 비밀(인증서 또는 암호)을 보호합니다. 주요 자격 증명 모음은 hello 키 관리 프로세스를 간소화 하는 데 도움이 됩니다 하 고 액세스 하 고 데이터를 암호화 하는 키의 toomaintain 제어 있습니다. 이 시나리오에서는 몇 가지 주요 자격 증명 모음 개념 toocreate 및 인증서 사용 소개, 방법에 대 한 철저 한 개요를 통해는 toouse 주요 자격 증명 모음입니다.

hello 단계를 수행 하는 방법을 보여 줍니다.

- Azure Key Vault 만들기
- 생성 또는 인증서 toohello 주요 자격 증명 모음 업로드
- Hello 인증서 tooinject tooa VM에서에서에서 암호 만들기
- VM을 만들고 hello 인증서 삽입

### <a name="create-an-azure-key-vault"></a>Azure Key Vault 만들기
먼저 [az keyvault create](/cli/azure/keyvault#create)를 사용하여 Key Vault를 만들고 VM 배포 시에 사용할 수 있도록 설정합니다. 각 Key Vault에는 고유한 이름이 필요하며 모두 소문자여야 합니다. 대체 *mykeyvault* 다음 예에서는 고유 키 자격 증명 모음 이름으로 hello에:

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a>인증서 생성 및 Key Vault에 저장
프로덕션 사용을 위해 [az keyvault certificate import](/cli/azure/keyvault/certificate#import)를 사용하여 신뢰할 수 있는 공급자가 서명한 유효한 인증서를 가져와야 합니다. 이 자습서에 대 한 hello 다음 예제와 자체 서명 된 인증서를 생성 하는 방법을 [az keyvault 인증서 만들기](/cli/azure/keyvault/certificate#create) hello 기본 인증서 정책을 사용 하 합니다.

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a>VM에 사용할 인증서 준비
hello VM 중 toouse hello 인증서 프로세스 만들기, 사용 하 여 인증서의 hello ID를 가져오려면 [az keyvault 비밀 목록-버전](/cli/azure/keyvault/secret#list-versions)합니다. hello VM hello 인증서가 필요는 특정 형식 tooinject 부팅에 있으므로 변환로 hello 인증서 [az vm 형식 비밀](/cli/azure/vm#format-secret)합니다. 다음 예제는 hello hello 출력 hello 사용 하 여 쉽게 이러한 명령 toovariables의 다음 단계에 할당 합니다.

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-toosecure-nginx"></a>클라우드 init config toosecure NGINX 만들기
인증서는 VM을 만들 시점과 키가 보호 하는 hello에 저장 */var/lib/waagent/* 디렉터리입니다. tooautomate 추가 hello 인증서 toohello VM 하 고 구성한 NGINX hello 이전 예제의 업데이트 된 클라우드 init config는 사용할 수 있습니다.

라는 파일을 만들어 *클라우드-init-secured.txt* 붙여넣기 hello 구성에 따라 합니다. 다시 클라우드 셸 hello를 사용 하는 경우 파일을 만듭니다 hello 클라우드 init 구성 없어 및 로컬 컴퓨터에 없습니다. 사용 하 여 `sensible-editor cloud-init-secured.txt` toocreate 파일 hello 및 사용할 수 있는 편집기의 목록을 확인 합니다. 해당 hello 전체 클라우드 init 파일을 올바르게 복사 했는지 확인, 특히 첫 번째 줄을 hello:

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-secure-vm"></a>보안 VM 만들기
이제 [az vm create](/cli/azure/vm#create)로 VM을 만듭니다. hello 인증서 데이터를 키 자격 증명 모음에서 hello로 주입 `--secrets` 매개 변수입니다. Hello 이전 예제와 같이 전달 hello로 hello 클라우드 init config `--custom-data` 매개 변수:

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-secured.txt \
    --secrets "$vm_secret"
```

Hello VM toobe 생성에 대 일 분 정도 걸리며 hello 패키지 tooinstall 및 hello 앱 toostart 합니다. Hello Azure CLI toohello 프롬프트 반환 된 후 toorun 계속 하는 백그라운드 작업 있습니다. 다른 몇 분 hello 앱에 액세스 하려면 먼저 수도 있습니다. Hello VM을 만들면 기록해 hello `publicIpAddress` hello Azure CLI로 표시 합니다. 이 주소는 웹 브라우저를 통해 사용 되는 tooaccess hello Node.js 응용 프로그램입니다.

tooallow 보안 웹 트래픽을 tooreach VM, 열린 포트 443에서 인터넷 hello와 [az vm-포트를 열](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a>보안 Web App 테스트
웹 브라우저를 열고 입력 수 이제 *https://<publicIpAddress>*  hello 주소 표시줄에 있습니다. 제공 하려면 사용자 고유의 공용 hello VM의에서 IP 주소를 만드는 프로세스입니다. 자체 서명 된 인증서를 사용 하는 경우 hello 보안 경고를 허용 합니다.

![웹 브라우저 보안 경고 허용](./media/tutorial-automate-vm-deployment/browser-warning.png)

보안 된 NGINX 사이트와 Node.js 앱 hello 다음 예제와 같이 표시 됩니다.

![실행 중인 보안 NGINX 사이트 보기](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a>다음 단계
이 자습서에서는 cloud-init를 사용하여 처음 부팅할 때 VM을 구성했습니다. 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * cloud-init 구성 파일 만들기
> * cloud-init 파일을 사용하는 VM 만들기
> * VM이 생성 하는 hello 후 실행 중인 Node.js 응용 프로그램 보기
> * 주요 자격 증명 모음 toosecurely 인증서 저장소를 사용 하 여
> * cloud-init를 사용하여 NGINX 배포 자동화

다음 자습서 toolearn toohello 어떻게 발전 toocreate 사용자 지정 VM 이미지입니다.

> [!div class="nextstepaction"]
> [사용자 지정 VM 이미지 만들기](./tutorial-custom-images.md)
