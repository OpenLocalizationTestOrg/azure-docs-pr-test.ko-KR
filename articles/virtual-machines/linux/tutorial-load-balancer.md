---
title: "Azure에서 Linux 가상 컴퓨터를 분산 하는 aaaHow tooload | Microsoft Docs"
description: "Toouse hello Azure Linux Vm의 경우 3 개 간에 분산 toocreate 항상 사용할 수 있으며 보안 응용 프로그램을 로드 하는 방법에 대해 알아봅니다"
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
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: f01752c3caec3489ee13e63000775769f3236e11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-linux-virtual-machines-in-azure-toocreate-a-highly-available-application"></a>어떻게 tooload 균형 toocreate Azure에서 Linux 가상 컴퓨터는 항상 사용 가능한 응용 프로그램
부하 분산은 들어오는 요청을 여러 가상 컴퓨터에 분산하여 높은 수준의 가용성을 제공합니다. 이 자습서에서는 hello의 여러 구성 요소가 hello Azure 부하 분산 장치 트래픽을 분산 및 고가용성을 제공 하는 방법에 대 한 설명입니다. 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * Azure Load Balancer 만들기
> * 부하 분산 장치 상태 프로브 만들기
> * 부하 분산 장치 트래픽 규칙 만들기
> * 클라우드 init toocreate 기본 Node.js 응용 프로그램을 사용 하 여
> * 가상 컴퓨터를 만들고 연결 하려면 tooa 부하 분산 장치
> * 부하 분산 장치의 실제 동작 보기
> * 부하 분산 장치에서 VM 추가 및 제거


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

## <a name="azure-load-balancer-overview"></a>Azure Load Balancer 개요
Azure Load Balancer는 들어오는 트래픽을 정상 VM 간에 분산하여 고가용성을 제공하는 계층 4(TCP, UDP) 부하 분산 장치입니다. 부하 분산 장치 상태 프로브 각 VM에서 특정된 포트를 모니터링 하 고 트래픽을 tooan 배포 VM 작동 합니다.

하나 이상의 공용 IP 주소를 포함하는 프런트 엔드 IP 구성을 정의할 수 있습니다. 이 프런트 엔드 IP 구성을 사용 하면 부하 분산 장치 및 응용 프로그램 toobe 액세스할 수 있는 hello 인터넷을 통해. 

가상 컴퓨터의 가상 네트워크 인터페이스 카드 (NIC)를 사용 하 여 tooa 부하 분산 장치를 연결 합니다. toodistribute 트래픽 toohello Vm, 백 엔드 주소 풀을 hello 가상 (Nic) 연결 된 toohello 부하 분산 장치의 hello IP 주소를 포함합니다.

트래픽 toocontrol hello 흐름을 정의한 특정 포트 및 프로토콜 tooyour Vm을 매핑하는 대 한 부하 분산 장치 규칙.

너무 hello 이전 자습서를 따른 경우[가상 컴퓨터 크기 집합을 만들](tutorial-create-vmss.md), 부하 분산 장치에 만들어진 합니다. 이러한 구성 요소가 모두 hello 크기 집합의 일부로 구성 되었습니다.


## <a name="create-azure-load-balancer"></a>Azure Load Balancer 만들기
이 섹션에는 만들어 hello 부하 분산 장치의 각 구성 요소를 구성 하는 방법을 자세히 설명 합니다. 부하 분산 장치를 만들려면 먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다. hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroupLoadBalancer* hello에 *eastus* 위치:

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a>공용 IP 주소 만들기
tooaccess 앱에서 인터넷 hello hello 부하 분산 장치에 대 한 공용 IP 주소를 사용 해야 합니다. [az network public-ip create](/cli/azure/network/public-ip#create)를 사용하여 공용 IP 주소를 만듭니다. hello 다음 예제에서는 명명 된 공용 IP 주소를 *myPublicIP* hello에 *myResourceGroupLoadBalancer* 리소스 그룹:

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a>부하 분산 장치 만들기
[az network lb create](/cli/azure/network/lb#create)를 사용하여 부하 분산 장치를 만듭니다. hello 다음 예제에서는 명명 된 부하 분산 장치 *myLoadBalancer* 및 할당 hello *myPublicIP* 주소 toohello 프런트 엔드 IP 구성:

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a>상태 프로브 만들기
tooallow hello 부하 분산 장치 toomonitor hello 상태 응용 프로그램의 상태 프로브를 사용 합니다. hello 상태 프로브는 동적으로 추가 하거나 Vm의 응답 toohealth 검사에 따라 hello 부하 분산 장치 순환에서 제거 합니다. 기본적으로 VM은 15 초 간격으로 두 개의 연속 된 실패 후 hello 부하 분산 장치 배포에서 제거 됩니다. 앱의 프로토콜 또는 특정 상태 확인 페이지에 따라 상태 프로브를 만듭니다. 

다음 예제는 hello TCP 프로브를 만듭니다. 좀 더 미세 조정된 상태 검사를 위해 사용자 지정 HTTP 프로브를 만들 수도 있습니다. 사용자 지정 HTTP 검색을 사용할 경우 만들어야 hello 상태 확인 페이지와 같은 *healthcheck.js*합니다. hello 프로브를 반환 해야 합니다는 **HTTP 200 OK** hello 부하 분산 장치 tookeep hello 호스트 회전에 대 한 응답입니다.

사용 하면 TCP 상태 프로브 toocreate [az 네트워크 lb 프로브 만들기](/cli/azure/network/lb/probe#create)합니다. hello 다음 예제에서는 명명 된 상태 프로브 *myHealthProbe*:

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a>부하 분산 장치 규칙 만들기
부하 분산 장치 규칙은 사용 되는 toodefine 트래픽 분산된 toohello Vm을가 하는 방법입니다. Hello 들어오는 트래픽의 캡슐화 된 트래픽과 hello 백 엔드 IP 풀 tooreceive hello, hello 필요한 원본 및 대상 포트에 대 한 프런트 엔드 IP 구성을 hello를 정의 합니다. 정상 Vm만 트래픽을 받도록 toomake, 또한 정의한 hello 상태 프로브 toouse 있습니다.

[az network lb rule create](/cli/azure/network/lb/rule#create)를 사용하여 부하 분산 장치 규칙을 만듭니다. hello 다음 규칙을 만드는 예제는 명명 된 *myLoadBalancerRule*를 사용 하 여 hello *myHealthProbe* 상태 프로브와 포트에서 트래픽을 잔액 *80*:

```azurecli-interactive 
az network lb rule create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myLoadBalancerRule \
    --protocol tcp \
    --frontend-port 80 \
    --backend-port 80 \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --probe-name myHealthProbe
```


## <a name="configure-virtual-network"></a>가상 네트워크 구성
일부 Vm을 배포 하 여 분산 장치를 테스트할 수 전에 가상 네트워크 리소스를 지 원하는 hello를 만듭니다. 가상 네트워크에 대 한 자세한 내용은 참조 hello [Azure 가상 네트워크 관리](tutorial-virtual-network.md) 자습서입니다.

### <a name="create-network-resources"></a>네트워크 리소스 만들기
[az network vnet create](/cli/azure/network/vnet#create)를 사용하여 가상 네트워크를 만듭니다. hello 다음 예제에서는 가상 네트워크를 만들어 명명 된 *myVnet* 이라는 서브넷과 *mySubnet*:

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

사용할 네트워크 보안 그룹 tooadd [az 네트워크 nsg 만들기](/cli/azure/network/nsg#create)합니다. hello 다음 예제에서는 네트워크 보안 그룹을 만든 라는 *myNetworkSecurityGroup*:

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

[az network nsg rule create](/cli/azure/network/nsg/rule#create)를 사용하여 네트워크 보안 그룹 규칙을 만듭니다. hello 다음 예제에서는 명명 된 네트워크 보안 그룹 규칙 *myNetworkSecurityGroupRule*:

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

가상 NIC는 [az network nic create](/cli/azure/network/nic#create)를 사용하여 만듭니다. hello 다음 예제에서는 세 개의 가상 Nic (각 VM에 대 한 가상 NIC 1 개에 대해 만드는 단계를 수행 하는 hello에서 응용 프로그램). 언제 든 지 가상 Nic를 추가 하 고 Vm을 만들 수 있고 toohello 부하 분산 장치를 추가할 수 없습니다.

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupLoadBalancer \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --network-security-group myNetworkSecurityGroup \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-virtual-machines"></a>가상 컴퓨터 만들기

### <a name="create-cloud-init-config"></a>cloud-init 구성 만들기
에 대 한 이전 자습서에서 [어떻게 toocustomize Linux 가상 컴퓨터를 처음 부팅할](tutorial-automate-vm-deployment.md), 방법에 대해 배웠습니다 클라우드 init로 tooautomate VM 사용자 지정 합니다. 에서는 동일한 클라우드 init 구성 파일 tooinstall NGINX hello 및 간단한 ' Hello World' Node.js 응용 프로그램을 실행 합니다.

현재 셸에서 라는 파일을 만들어 *클라우드 init.txt* 붙여넣기 hello 구성에 따라 합니다. 예를 들어 로컬 컴퓨터에 없는 클라우드 셸 hello에 hello 파일을 만듭니다. 입력 `sensible-editor cloud-init.txt` toocreate 파일 hello 및 사용할 수 있는 편집기의 목록을 확인 합니다. 해당 hello 전체 클라우드 init 파일을 올바르게 복사 했는지 확인, 특히 첫 번째 줄을 hello:

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

### <a name="create-virtual-machines"></a>가상 컴퓨터 만들기
tooimprove hello 고가용성 응용 프로그램의 가용성 집합에 Vm을 배치 합니다. 가용성 집합에 대 한 자세한 내용은 참조 hello 이전 [어떻게 toocreate 항상 사용 가능한 가상 컴퓨터](tutorial-availability-sets.md) 자습서입니다.

[az vm availability-set create](/cli/azure/vm/availability-set#create)를 사용하여 가용성 집합을 만듭니다. hello 다음 예제에서는 가용성 명명 된 집합 *myAvailabilitySet*:

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

Hello Vm을 만들 수 이제 [az vm 만들기](/cli/azure/vm#create)합니다. hello 다음 예제에서는 세 개의 Vm 만들고 이미 존재 하지 않는 경우에 SSH 키를 생성 합니다.

```bash
for i in `seq 1 3`; do
    az vm create \
        --resource-group myResourceGroupLoadBalancer \
        --name myVM$i \
        --availability-set myAvailabilitySet \
        --nics myNic$i \
        --image UbuntuLTS \
        --admin-username azureuser \
        --generate-ssh-keys \
        --custom-data cloud-init.txt \
        --no-wait
done
```

Hello Azure CLI toohello 프롬프트 반환 된 후 toorun 계속 하는 백그라운드 작업 있습니다. hello `--no-wait` 작업 toocomplete hello 모두에 대 한 매개 변수를 대기 하지 않습니다. 다른 몇 분 hello 앱에 액세스 하려면 먼저 수도 있습니다. hello 부하 분산 장치 상태 프로브 때 자동으로 검색 각 VM에서 hello 응용 프로그램을 실행 합니다. Hello 앱이 실행 되 면 hello 부하 분산 장치 규칙 toodistribute 트래픽을 시작 합니다.


## <a name="test-load-balancer"></a>부하 분산 장치 테스트
Hello 있는 부하 분산 장치 프로그램의 공용 IP 주소 가져오기 [az 네트워크 공개 ip 표시](/cli/azure/network/public-ip#show)합니다. hello 다음 예제에서는 가져옵니다 hello IP 주소를 *myPublicIP* 앞에서 만든:

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

그런 다음 tooa 웹 브라우저에서 hello 공용 IP 주소를 입력할 수 있습니다. 기억-hello 부하 분산 장치 toodistribute 트래픽 toothem를 시작 하기 전에 몇 분 hello hello Vm toobe 준비를 사용 합니다. hello 앱이 표시 됩니다, 그리고 hello VM의 hello 호스트 이름을 포함 하 여 해당 hello 부하 분산 장치는 hello 다음 예제에서에서 트래픽 tooas 분산:

![Node.js 앱 실행](./media/tutorial-load-balancer/running-nodejs-app.png)

응용 프로그램을 실행 하는 모든 세 개의 Vm에 트래픽을 분산 toosee hello에 대 한 부하 분산 장치, 있습니다 수 강제 새로 고침 웹 브라우저입니다.


## <a name="add-and-remove-vms"></a>VM 추가 및 제거
Hello OS 업데이트를 설치 하는 등의 응용 프로그램을 실행 하는 Vm에 tooperform 유지 관리를 할 수 있습니다. 늘어난된 트래픽 tooyour 앱과 toodeal, tooadd 할 수 있습니다 추가 Vm입니다. 이 섹션에서는 tooremove 하거나 hello 부하 분산 장치에서 VM을 추가 합니다.

### <a name="remove-a-vm-from-hello-load-balancer"></a>Hello 부하 분산 장치에서 VM을 제거 합니다.
Hello 백 엔드 주소 풀을에서 VM을 제거할 수 있습니다 [az 네트워크 nic ip 구성 주소 풀 제거](/cli/azure/network/nic/ip-config/address-pool#remove)합니다. 다음 예제를 제거 하는 hello hello에 대 한 가상 NIC **myVM2** 에서 *myLoadBalancer*:

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

나머지 두 hello에 트래픽을 분산 toosee hello에 대 한 부하 분산 장치 앱을 실행 하는 Vm 있습니다 수 강제 새로 고침 웹 브라우저입니다. 이제 hello OS 업데이트를 설치 하 여 VM 다시 부팅 수행 등 VM에 유지 관리를 수행할 수 있습니다.

### <a name="add-a-vm-toohello-load-balancer"></a>VM toohello 부하 분산 장치 추가
VM 유지 관리를 수행한 후 tooexpand 용량이 필요한 경우 사용 하 여 VM toohello 백 엔드 주소 풀을 추가할 수 있습니다 또는 [az 네트워크 nic ip 구성 주소 풀 추가](/cli/azure/network/nic/ip-config/address-pool#add)합니다. hello 다음 예제에서는 추가 hello에 대 한 가상 NIC **myVM2** 너무*myLoadBalancer*:

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a>다음 단계
이 자습서에서는 부하 분산 장치 만들고 Vm tooit 첨부 합니다. 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * Azure Load Balancer 만들기
> * 부하 분산 장치 상태 프로브 만들기
> * 부하 분산 장치 트래픽 규칙 만들기
> * 클라우드 init toocreate 기본 Node.js 응용 프로그램을 사용 하 여
> * 가상 컴퓨터를 만들고 연결 하려면 tooa 부하 분산 장치
> * 부하 분산 장치의 실제 동작 보기
> * 부하 분산 장치에서 VM 추가 및 제거

Azure 가상 네트워크 구성 요소에 대 한 자세한 toohello 다음 자습서 toolearn를 진행 합니다.

> [!div class="nextstepaction"]
> [VM 및 가상 네트워크 관리](tutorial-virtual-network.md)
