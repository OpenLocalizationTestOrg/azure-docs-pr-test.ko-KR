---
title: "Azure에서 linux 가상 컴퓨터 크기 집합 aaaCreate | Microsoft Docs"
description: "가상 컴퓨터 확장 집합을 사용하여 Linux VM에 항상 사용 가능한 응용 프로그램을 만들고 배포합니다."
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.openlocfilehash: 00dd81043f9be46ef2dc6dfe97eefdb20944ee13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a>가상 컴퓨터 확장 집합 만들기 및 Linux에 항상 사용 가능한 앱 배포
가상 컴퓨터 크기 집합 toodeploy 있으며, 자동 크기 조정 동일한 가상 컴퓨터를 관리 합니다. 수동으로 hello hello 크기 집합의 Vm 수의 크기를 조정 하거나 기반으로 CPU 사용량, 메모리 수요가 또는 네트워크 트래픽 규칙 tooautoscale 정의할 수 있습니다. 이 자습서에서는 Azure에서 가상 컴퓨터 확장 집합을 배포합니다. 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * 클라우드 init toocreate 앱 tooscale 사용
> * 가상 컴퓨터 확장 집합 만들기
> * Hello 크기 집합의 인스턴스 수를 늘리거나
> * 확장 집합 인스턴스에 대한 연결 정보 보기
> * 확장 집합에 데이터 디스크 사용


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

## <a name="scale-set-overview"></a>확장 집합 개요
가상 컴퓨터 크기 집합 toodeploy 있으며, 자동 크기 조정 동일한 가상 컴퓨터를 관리 합니다. 크기 조정 설정 사용 하 여 hello 동일한 구성 요소 hello 이전 자습서에서 너무 배운[항상 사용 가능한 Vm을 만들](tutorial-availability-sets.md)합니다. 확장 집합의 VM은 가용성 집합에 만들어지고 논리 장애 도메인 및 업데이트 도메인에 분산됩니다.

VM은 필요에 따라 확장 집합에 생성됩니다. 자동 크기 조정 규칙 toocontrol 정의 방법 및 시기 Vm 더하거나 hello 크기 집합에서 제거 합니다. 이러한 규칙은 메트릭(예: CPU 부하, 메모리 사용량 또는 네트워크 트래픽)을 기반으로 트리거할 수 있습니다.

크기 조정 설정 too1, 000 Vm Azure 플랫폼 이미지 사용을 지원 합니다. 프로덕션 작업에 대해 지정할 수 있습니다 너무[사용자 지정 VM 이미지를 만들](tutorial-custom-images.md)합니다. Too100 vm 크기 집합 사용자 지정 이미지를 사용 하는 경우에 만들 수 있습니다.


## <a name="create-an-app-tooscale"></a>응용 프로그램 tooscale 만들기
프로덕션 용도로 수도 있습니다 너무[사용자 지정 VM 이미지를 만들](tutorial-custom-images.md) 응용 프로그램 설치 및 구성 포함 합니다. 이 자습서에 대 한 첫 번째 부팅 tooquickly에 있는 Vm 크기 집합 작업에서 참조 하는 hello를 사용자 지정할 수 있습니다.

이전 자습서에서 배운 [어떻게 toocustomize Linux 가상 컴퓨터를 처음 부팅할](tutorial-automate-vm-deployment.md) 클라우드 init로 합니다. 에서는 동일한 클라우드 init 구성 파일 tooinstall NGINX hello 및 간단한 ' Hello World' Node.js 응용 프로그램을 실행 합니다. 

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


## <a name="create-a-scale-set"></a>확장 집합 만들기
확장 집합을 만들려면 먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다. hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroupScaleSet* hello에 *eastus* 위치:

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

이제 [az vmss create](/cli/azure/vmss#create)를 사용하여 가상 컴퓨터 확장 집합을 만듭니다. hello 다음 예제에서는 크기 명명 된 집합 *myScaleSet*hello 클라우드 init 파일 toocustomize hello VM을 사용 하 고 존재 하지 않는 경우 SSH 키를 생성 합니다.

```azurecli-interactive 
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image UbuntuLTS \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

몇 분 toocreate 걸리고 모든 hello 눈금 집합 리소스와 Vm을 구성 합니다. Hello Azure CLI toohello 프롬프트 반환 된 후 toorun 계속 하는 백그라운드 작업 있습니다. 다른 몇 분 hello 앱에 액세스 하려면 먼저 수도 있습니다.


## <a name="allow-web-traffic"></a>웹 트래픽 허용
부하 분산 장치는 hello 가상 컴퓨터 크기 집합의 일부로 자동으로 생성 되었습니다. hello 부하 분산 장치 부하 분산 장치 규칙을 사용 하 여 정의 된 Vm의 조합에 대해 트래픽을 분산 시킵니다. 부하 분산 장치 개념과 hello 다음 자습서에서는 구성에 대 한 자세히 알아볼 수 있습니다 [tooload Azure의 가상 컴퓨터를 분산 하는 방법을](tutorial-load-balancer.md)합니다.

tooallow 트래픽 tooreach hello 웹 앱을 사용 하는 규칙을 만들 [az 네트워크 lb 규칙 만들기](/cli/azure/network/lb/rule#create)합니다. hello 다음 규칙을 만드는 예제는 명명 된 *myLoadBalancerRuleWeb*:

```azurecli-interactive 
az network lb rule create \
  --resource-group myResourceGroupScaleSet \
  --name myLoadBalancerRuleWeb \
  --lb-name myScaleSetLB \
  --backend-pool-name myScaleSetLBBEPool \
  --backend-port 80 \
  --frontend-ip-name loadBalancerFrontEnd \
  --frontend-port 80 \
  --protocol tcp
```

## <a name="test-your-app"></a>앱 테스트
toosee hello 웹에서 Node.js 응용 프로그램으로 부하 분산 장치의 hello 공용 IP 주소를 가져올 [az 네트워크 공개 ip 표시](/cli/azure/network/public-ip#show)합니다. hello 다음 예제에서는 가져옵니다 hello IP 주소를 *myScaleSetLBPublicIP* hello 크기 집합의 일부로 만들어집니다.

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

Tooa 웹 브라우저에서 hello 공용 IP 주소를 입력 합니다. hello 앱 hello 해당 VM을 분산 장치 배포 트래픽의 부하를 hello의 hello 호스트 이름을 포함 하 여 표시 됩니다.

![Node.js 앱 실행](./media/tutorial-create-vmss/running-nodejs-app.png)

작업에서 설정 toosee hello 눈금 있습니다 수 강제 새로 고침 웹 브라우저 toosee hello 부하 분산 장치 앱을 실행 하는 모든 hello Vm 트래픽을 분산 합니다.


## <a name="management-tasks"></a>관리 작업
Hello 크기 집합의 hello 수명 주기 동안 toorun 할 수 있습니다 하나 이상의 관리 작업입니다. 또한 다양 한 수명 주기 작업을 자동화 하는 toocreate 스크립트를 지정할 수 있습니다. hello Azure CLI 2.0 신속 하 게 toodo 이러한 작업을 제공합니다. 다음은 몇 가지 일반적인 작업입니다.

### <a name="view-vms-in-a-scale-set"></a>확장 집합의 VM 보기
tooview 눈금에서 실행 중인 Vm의 목록 설정, 사용 하 여 [az vmss 목록 인스턴스](/cli/azure/vmss#list-instances) 다음과 같습니다.

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

hello 비슷한 toohello 다음은 예제 출력:

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a>VM 인스턴스 증가 또는 감소
인스턴스의 toosee hello 수 현재는 규모에 맞게 설정, 사용 하 여 [az vmss 표시](/cli/azure/vmss#show) 에서 쿼리 및 *sku.capacity*:

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

있습니다 다음 수동으로 거 나 낮출 수로 설정 하는 hello 규모에 맞게 가상 컴퓨터의 hello 수 [az vmss 확장](/cli/azure/vmss#scale)합니다. hello 다음 예제에서는 설정 hello Vm 수 너무 설정 하 여 규모에 맞게*5*:

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

자동 크기 조정 규칙 tooscale hello 눈금에서 Vm 수의 위아래로 예: 네트워크 트래픽 또는 CPU 사용량 응답 toodemand에서 설정 하는 방법을 정의할 수 있습니다. 현재 이 규칙은 Azure CLI 2.0에서 설정할 수 없습니다. 사용 하 여 hello [Azure 포털](https://portal.azure.com) tooconfigure 자동 크기 조정 합니다.

### <a name="get-connection-info"></a>연결 정보 가져오기
tooobtain 연결 정보에 대 한 Vm 크기 집합의 hello, 사용 하 여 [az vmss 목록-인스턴스-연결-정보](/cli/azure/vmss#list-instance-connection-info)합니다. 이 명령은 tooconnect SSH 사용 하면 각 VM에 대 한 hello 공용 IP 주소와 포트를 출력 합니다.

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a>확장 집합으로 데이터 디스크 사용
확장 집합으로 데이터 디스크를 사용할 수 있습니다. 이전 자습서에서 배운 너무 어떻게[관리 Azure 디스크](tutorial-manage-disks.md) 윤곽선 hello 모범 사례 및 hello 운영 체제 디스크 대신 데이터 디스크에 앱을 빌드하기 위한 성능 향상을 합니다.

### <a name="create-scale-set-with-data-disks"></a>데이터 디스크로 확장 집합 만들기
소수 자릿수를 설정 하 고 데이터 디스크 연결 toocreate hello 추가 `--data-disk-sizes-gb` 매개 변수 toohello [az vmss 만들기](/cli/azure/vmss#create) 명령입니다. hello 다음 예제에서는 사용 하 여 설정 하는 눈금 *50*Gb 데이터 디스크가 연결 tooeach 인스턴스:

```azurecli-interactive 
az vmss create \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetDisks \
    --image UbuntuLTS \
    --upgrade-policy-mode automatic \
    --custom-data cloud-init.txt \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50
```

확장 집합에서 인스턴스가 제거되면 연결된 데이터 디스크도 제거됩니다.

### <a name="add-data-disks"></a>데이터 디스크 추가
사용 하 여 tooadd 눈금에 데이터 디스크 tooinstances 설정 [az vmss 디스크 연결](/cli/azure/vmss/disk#attach)합니다. hello 다음 예제에서는 추가 *50*Gb 디스크 tooeach 인스턴스:

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a>데이터 디스크 분리
사용 하 여 tooremove 눈금에 데이터 디스크 tooinstances 설정 [az vmss 디스크 분리](/cli/azure/vmss/disk#detach)합니다. hello 다음 예제에서는 제거 hello 데이터 디스크 LUN에 *2* 각 인스턴스에서:

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a>다음 단계
이 자습서에서는 가상 컴퓨터 확장 집합을 만들었습니다. 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * 클라우드 init toocreate 앱 tooscale 사용
> * 가상 컴퓨터 확장 집합 만들기
> * Hello 크기 집합의 인스턴스 수를 늘리거나
> * 확장 집합 인스턴스에 대한 연결 정보 보기
> * 확장 집합에 데이터 디스크 사용

부하 분산 가상 컴퓨터에 대 한 개념에 대 한 자세한 toohello 다음 자습서 toolearn를 진행 합니다.

> [!div class="nextstepaction"]
> [Virtual Machines 부하 분산](tutorial-load-balancer.md)