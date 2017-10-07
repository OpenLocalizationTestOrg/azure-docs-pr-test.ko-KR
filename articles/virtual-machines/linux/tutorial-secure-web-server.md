---
title: "Azure에서 웹 서버 ssl 인증서 aaaSecure | Microsoft Docs"
description: "Azure에서 Linux VM의 toosecure hello NGINX 웹 서버 ssl 인증서 하는 방법을 알아봅니다"
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
ms.date: 07/17/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: d3a62d77ac05c9aa2a44356b7c8e44cb485b81aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a>Azure에서 Linux 가상 컴퓨터의 SSL 인증서로 웹 서버 보호
toosecure 웹 서버, 나중에 SSL (Secure Sockets) 인증서 수 tooencrypt 웹 트래픽을 사용 합니다. 이 SSL 인증서 Azure 키 자격 증명 모음에 저장할 수 있으며 Azure에서 인증서 tooLinux 가상 컴퓨터 (Vm)의 보안 배포를 허용 합니다. 이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * Azure Key Vault 만들기
> * 생성 또는 인증서 toohello 주요 자격 증명 모음 업로드
> * VM을 만들고 hello NGINX 웹 서버를 설치 합니다.
> * Hello VM hello 인증서 삽입 하 고을 SSL 바인딩과 함께 NGINX 구성

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.  


## <a name="overview"></a>개요
Azure Key Vault는 암호화 키 및 비밀 정보(인증서 또는 암호)를 보호합니다. 주요 자격 증명 모음은 hello 인증서 관리 프로세스를 간소화 하는 데 도움이 됩니다 하 고 해당 인증서에 액세스 하는 키의 toomaintain 제어 있습니다. Key Vault 내에 자체 서명된 인증서를 만들거나 이미 소유하고 있는 기존의 신뢰할 수 있는 인증서를 업로드할 수 있습니다.

내재된 인증서를 포함하는 사용자 지정 VM 이미지를 사용하는 대신 실행 중인 VM에 인증서를 삽입합니다. 이 프로세스 hello 최신 인증서 배포 하는 동안 웹 서버에 설치 되어 있는지 확인 합니다. 인증서를 바꾸거나 갱신도 없으면 toocreate 새 사용자 지정 VM 이미지입니다. hello 최신 인증서는 추가 Vm을 만들 때 자동으로 삽입 됩니다. Hello 전체 과정 hello 인증서 되지 hello Azure 플랫폼에서 나 가지 스크립트, 명령줄 기록 또는 서식 파일에 표시 됩니다.


## <a name="create-an-azure-key-vault"></a>Azure Key Vault 만들기
Key Vault 및 인증서를 만들려면 먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다. hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroupSecureWeb* hello에 *eastus* 위치:

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

다음으로 [az keyvault create](/cli/azure/keyvault#create)를 사용하여 Key Vault를 만들고 VM 배포 시에 사용할 수 있도록 설정합니다. 각 Key Vault에는 고유한 이름이 필요하며 모두 소문자여야 합니다. 대체 * <mykeyvault> * 다음 예에서는 고유 키 자격 증명 모음 이름으로 hello에:

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a>인증서 생성 및 Key Vault에 저장
프로덕션 사용을 위해 [az keyvault certificate import](/cli/azure/certificate#import)를 사용하여 신뢰할 수 있는 공급자가 서명한 유효한 인증서를 가져와야 합니다. 이 자습서에 대 한 hello 다음 예제와 자체 서명 된 인증서를 생성 하는 방법을 [az keyvault 인증서 만들기](/cli/azure/certificate#create) hello 기본 인증서 정책을 사용 하 합니다.

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a>VM에 사용할 인증서 준비
hello VM 중 toouse hello 인증서 프로세스 만들기, 사용 하 여 인증서의 hello ID를 가져오려면 [az keyvault 비밀 목록-버전](/cli/azure/keyvault/secret#list-versions)합니다. Hello 인증서와 변환 [az vm 형식 비밀](/cli/azure/vm#format-secret)합니다. 다음 예제는 hello hello 출력 hello 사용 하 여 쉽게 이러한 명령 toovariables의 다음 단계에 할당 합니다.

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-toosecure-nginx"></a>클라우드 init config toosecure NGINX 만들기
[클라우드 init](https://cloudinit.readthedocs.io) 는 널리 사용 되는 접근 방식을 toocustomize Linux VM 처음으로 hello에 대 한 부팅 합니다. 클라우드 init tooinstall 패키지를 사용할 수 있으며 파일, 또는 tooconfigure 사용자 및 보안에 기록할 수 있습니다. 추가 단계 없이 없는 클라우드 init hello 초기 부팅 프로세스 중 실행 될 때 또는 에이전트 tooapply 구성에 필요 합니다.

인증서는 VM을 만들 시점과 키가 보호 하는 hello에 저장 */var/lib/waagent/* 디렉터리입니다. tooautomate 추가 hello 인증서 toohello VM 및 클라우드 초기화에 사용 하 여 hello 웹 서버를 구성 합니다. 이 예제에서는 설치 하 고 hello NGINX 웹 서버를 구성 합니다. Hello를 사용할 수 있습니다 tooinstall를 처리 하 고 Apache 구성 동일 합니다. 

라는 파일을 만들어 *init 웹 server.txt 클라우드* 붙여넣기 hello 구성에 따라:

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
      }
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
```

### <a name="create-a-secure-vm"></a>보안 VM 만들기
이제 [az vm create](/cli/azure/vm#create)로 VM을 만듭니다. hello 인증서 데이터를 키 자격 증명 모음에서 hello로 주입 `--secrets` 매개 변수입니다. Hello로 hello init 클라우드 구성에 전달 하면 `--custom-data` 매개 변수:

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-web-server.txt \
    --secrets "$vm_secret"
```

Hello VM toobe 생성에 대 일 분 정도 걸리며 hello 패키지 tooinstall 및 hello 앱 toostart 합니다. Hello VM을 만들면 기록해 hello `publicIpAddress` hello Azure CLI로 표시 합니다. 이 주소는 사용 되는 tooaccess 웹 브라우저에서 사이트입니다.

tooallow 보안 웹 트래픽을 tooreach VM, 열린 포트 443에서 인터넷 hello와 [az vm-포트를 열](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-hello-secure-web-app"></a>Hello 보안 웹 응용 프로그램 테스트
웹 브라우저를 열고 입력 수 이제 *https://<publicIpAddress> * hello 주소 표시줄에 있습니다. 제공 하려면 사용자 고유의 공용 hello VM의에서 IP 주소를 만드는 프로세스입니다. 자체 서명 된 인증서를 사용 하는 경우 hello 보안 경고를 허용 합니다.

![웹 브라우저 보안 경고 허용](./media/tutorial-secure-web-server/browser-warning.png)

보안 된 NGINX 사이트 hello 다음 예제와 같이 표시 됩니다.

![실행 중인 보안 NGINX 사이트 보기](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a>다음 단계

이 자습서에서는 Azure Key Vault에 저장된 SSL 인증서를 사용하여 NGINX 웹 서버를 보호했습니다. 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * Azure Key Vault 만들기
> * 생성 또는 인증서 toohello 주요 자격 증명 모음 업로드
> * VM을 만들고 hello NGINX 웹 서버를 설치 합니다.
> * Hello VM hello 인증서 삽입 하 고을 SSL 바인딩과 함께 NGINX 구성

가상 컴퓨터 스크립트 샘플을 미리 만들어진이 링크 toosee를 따릅니다.

> [!div class="nextstepaction"]
> [Windows 가상 컴퓨터 스크립트 샘플 ](./cli-samples.md)