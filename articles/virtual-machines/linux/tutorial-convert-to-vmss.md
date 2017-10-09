---
title: "aaaConvert 하는 Azure VM tooa 범위로 설정 | Microsoft Docs"
description: "만들고 hello Azure CLI를 사용 하 여 설정 Linux Azure 가상 컴퓨터 크기를 배포 합니다."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 04/05/2017
ms.author: adegeo
ms.openlocfilehash: e228282ac4855cef589b8500e74e9d461f9aed84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-an-existing-azure-virtual-machine-tooa-scale-set"></a>기존 Azure 가상 컴퓨터 tooa 눈금 집합으로 변환

이 자습서는 가상 컴퓨터 tooa 가상 컴퓨터 크기 설정 하는 Azure CLI 2.0 toouse tooconvert 방법을 보여 줍니다. 또한 hello 규모에 맞게 hello 가상 컴퓨터의 tooautomate hello 구성을 설정 하는 방법을 알아봅니다. Tooinstall Azure CLI 2.0을 확인 하려면 어떻게 해야 대 한 자세한 내용은 [Azure CLI 2.0 시작](/cli/azure/get-started-with-azure-cli.md)합니다. 규모 집합에 대한 자세한 내용은 [가상 컴퓨터 규모 집합](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)을 참조하세요.

## <a name="step-1---deprovision-hello-vm"></a>1 단계-Deprovision hello VM

SSH tooconnect toohello VM을 사용 합니다.

프로 비전 해제 hello VM hello Azure VM 에이전트 toodelete 파일 및 데이터를 사용 하 여 합니다. 프로비전 해제에 대한 세부적인 개요는 [Linux 가상 컴퓨터 캡처](capture-image.md)를 참조하세요.

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-hello-vm"></a>2 단계-hello VM의 이미지 캡처

캡처에 대한 세부적인 개요는 [Linux 가상 컴퓨터 캡처](capture-image.md)를 참조하세요.

Deallocate의 VM hello [az vm 할당을 취소](/cli/azure/vm#deallocate):

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

일반화의 VM hello [az vm 일반화](/cli/azure/vm#generalize):

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

사용 하 여 hello VM 리소스에서 이미지 만들기 [az 이미지 만들기](/cli/azure/image#create):

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-hello-scale-set"></a>3 단계-hello 크기 집합 만들기

Hello 가져오기 **id** hello 이미지의 합니다.

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

[az vm create](/cli/azure/vmss#create)를 사용하여 이미지 리소스에서 VM을 만듭니다.

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

이 명령은 10GB 데이터 디스크도 연결합니다. Hello VM에 따라 선택한 크기는 (사용 **Standard_DS1_v2**), 허용 되는 데이터 디스크의 hello 번호가 다르면 합니다. 자세한 내용을 보려면 검토 hello [가상 컴퓨터 크기](sizes.md)합니다.

Hello 배율 설정 완료 되 면 tooit을 연결 합니다. 와 SSH에 대 한 hello 인스턴스 IP 주소의 목록을 가져올 [az vmss 목록-인스턴스-연결-정보](/cli/azure/vmss#list-instance-connection-info):

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

이제 toohello 가상 컴퓨터 인스턴스 tooinitialize hello 데이터 디스크를 연결할 수 있습니다.

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-hello-data-disk"></a>4 단계-hello 데이터 디스크 초기화

연결 된 toohello 가상 컴퓨터를 하는 동안와 hello 디스크 파티션 `fdisk`:

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

Hello로 파일 시스템 toohello 파티션에 쓰기 `mkfs` 명령:

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Hello 운영 체제에 액세스할 수 있도록 hello 새 디스크를 탑재 합니다.

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

hello 디스크 hello datadrive 탑재 지점,으로 확인할 수 있습니다를 통해 액세스 될 수 있습니다 `ls /datadrive/`합니다.

Hello SSH 세션을 종료 합니다.


## <a name="step-5---configure-firewall"></a>5단계 - 방화벽 구성

Hello 방화벽 toohello 웹 서버 hello 크기 집합에서 호스트를 통해 구멍을 펀치 합니다. Hello 크기 집합 만들었고, 부하 분산 장치도 생성을 사용 하는 경우 **SSH** toohello 개별 가상 컴퓨터. 두 가지 정보를 얻을 수 해야 포트 tooopen Azure CLI를 사용 하 여 합니다.

* **프런트 엔드 IP 주소 풀**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* **백 엔드 IP 주소 풀**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

이러한 두 가지 이름을 사용하여 포트 **80**을 열 수 있습니다.

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a>6단계 – 구성 자동화

hello 데이터 디스크 toobe 각 가상 컴퓨터 인스턴스에서 구성 해야 합니다. Hello로 hello 가상 컴퓨터의 hello 구성을 자동화할 수 우리 **CustomScript** 확장 합니다.

먼저 만듭니다는 *.sh* hello 디스크 형식 명령을 포함 하는 스크립트입니다.

```sh
#!/bin/bash

# Setup hello data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

그런 다음 해당 스크립트 파일 toowhere hello 업로드 **CustomScript** 확장에 액세스할 수 있습니다. 복사본은 [여기](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4)에 있습니다.

라는 로컬 파일을 만들어 **settings.json** put hello JSON 블록에 다음 및 합니다. hello `flieUris` 속성을 설정 해야 toowhere 스크립트 파일에 업로드 되었습니다.

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

이 명령은 tooyour 규모 hello를 사용 하 여 설정 배포 **CustomScript** hello 참조 확장 **settings.json** 방금 만든 파일입니다.

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

이 확장은 현재의 모든 인스턴스와 나중에 크기 조정에 의해 생성되는 모든 인스턴스에서 자동으로 실행됩니다.

## <a name="step-7---configure-autoscale-rules"></a>7단계 - 자동 크기 조정 규칙 구성

현재 자동 크기 조정 규칙은 Azure CLI에서 설정할 수 없습니다. 사용 하 여 hello [Azure 포털](https://portal.azure.com) tooconfigure 자동 크기 조정 합니다.

## <a name="step-8---management-tasks"></a>8단계 - 관리 작업

Hello 크기 집합의 hello 수명 주기 동안 toorun 할 수 있습니다 하나 이상의 관리 작업입니다. 또한 다양 한 수명 주기 작업을 자동화 하는 toocreate 스크립트 할 수도 있습니다 하 고 hello Azure CLI 신속 하 게 toodo를 해당 작업 제공 합니다. 다음은 몇 가지 일반적인 작업입니다.

### <a name="get-connection-info"></a>연결 정보 가져오기

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a>인스턴스 수 설정(수동 크기 조정)

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a>리소스 그룹 삭제

리소스 그룹을 삭제하면 그 안에 포함된 리소스도 모두 삭제됩니다.

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>다음 단계
이 자습서에 도입 된 기능을 설정 hello 가상 컴퓨터 크기 중 일부에 대 한 자세한 toolearn hello 다음 정보를 참조 하십시오.

- [Azure Virtual Machine Scale Sets 개요](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [Azure Load Balancer개요](../../load-balancer/load-balancer-overview.md)
- [네트워크 보안 그룹을 사용하여 네트워크 트래픽 흐름 제어](../../virtual-network/virtual-networks-nsg.md)