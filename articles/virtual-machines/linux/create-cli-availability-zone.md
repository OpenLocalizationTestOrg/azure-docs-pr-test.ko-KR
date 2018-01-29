---
title: "Azure CLI를 사용하여 영역 설정된 Linux VM 만들기 | Microsoft Docs"
description: "Azure CLI를 사용하여 가용성 영역에서 Linux VM 만들기"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 09/19/2017
ms.author: danlep
ms.custom: 
ms.openlocfilehash: 5e742187295d0bd6dbc0767ee164335fc0cf9f02
ms.sourcegitcommit: 3cdc82a5561abe564c318bd12986df63fc980a5a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/05/2018
---
# <a name="create-a-linux-virtual-machine-in-an-availability-zone-with-the-azure-cli"></a>Azure CLI를 사용하여 가용성 영역에서 Linux 가상 머신 만들기

이 문서는 Azure CLI를 사용하여 Azure 가용성 영역에서 Linux VM을 만드는 단계를 안내합니다. [가용성 영역](../../availability-zones/az-overview.md)은 Azure 지역에서 물리적으로 별도 영역입니다. 가용성 영역을 사용하여 가능성이 적은 실패 또는 전체 데이터 센터의 손실로부터 앱 및 데이터를 보호합니다.

[!INCLUDE [availability-zones-preview-statement.md](../../../includes/availability-zones-preview-statement.md)]

최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치했고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인했는지 확인합니다.


## <a name="check-vm-sku-availability"></a>VM SKU 가용성 확인
VM 크기 또는 SKU의 가용성은 지역 및 영역에 따라 다를 수 있습니다. 가용성 영역 사용을 계획하는 데 도움이 되도록 Azure 지역 및 영역별로 사용 가능한 VM SKU를 나열할 수 있습니다. 이 기능을 사용하면 적절한 VM 크기를 선택하고 영역 간에 원하는 복원력을 얻을 수 있습니다. 다른 VM 유형 및 크기에 대한 자세한 내용은 [VM 크기 개요](sizes.md)를 참조하세요.

[az vm list-skus](/cli/azure/vm#az_vm_list_skus) 명령으로 사용 가능한 VM SkU를 볼 수 있습니다. 다음 예제에서는 *eastus2* 지역에서 사용 가능한 VM SKU를 나열합니다.

```azurecli
az vm list-skus --location eastus2 --output table
```

출력은 다음과 같이 압축된 예제와 비슷하며, 각 VM 크기를 사용할 수 있는 가용성 영역을 보여 줍니다.

```azurecli
ResourceType      Locations  Name               Tier       Size     Zones
----------------  ---------  -----------------  ---------  -------  -------
virtualMachines   eastus2    Standard_DS1_v2    Standard   DS1_v2   1,2,3
virtualMachines   eastus2    Standard_DS2_v2    Standard   DS2_v2   1,2,3
[...]
virtualMachines   eastus2    Standard_F1s       Standard   F1s      1,2,3
virtualMachines   eastus2    Standard_F2s       Standard   F2s      1,2,3
[...]
virtualMachines   eastus2    Standard_D2s_v3    Standard   D2_v3    1,2,3
virtualMachines   eastus2    Standard_D4s_v3    Standard   D4_v3    1,2,3
[...]
virtualMachines   eastus2    Standard_E2_v3     Standard   E2_v3    1,2,3
virtualMachines   eastus2    Standard_E4_v3     Standard   E4_v3    1,2,3
```


## <a name="create-resource-group"></a>리소스 그룹 만들기

[az group create](/cli/azure/group#az_group_create) 명령을 사용하여 리소스 그룹을 만듭니다.  

Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다. 가상 머신보다 먼저 리소스 그룹을 만들어야 합니다. 이 예제에서는 *eastus2* 지역에 *myResourceGroupVM*이라는 리소스 그룹을 만듭니다. 미국 동부 2는 미리 보기에서 가용성 영역을 지원하는 Azure 지역 중 하나입니다.

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus2
```

리소스 그룹은 VM을 만들거나 수정할 때 지정되며 이 문서 전체에서 확인할 수 있습니다.

## <a name="create-virtual-machine"></a>가상 컴퓨터 만들기

[az vm create](/cli/azure/vm#az_vm_create) 명령을 사용하여 가상 머신을 만듭니다. 

가상 머신을 만들 때 운영 체제 이미지, 디스크 크기 조정 및 관리 자격 증명 등의 몇 가지 옵션을 사용할 수 있습니다. 이 예제에서는 Ubuntu Server를 실행하는 *myVM*이라는 가상 머신을 만듭니다. VM은 가용성 영역 *1*에서 생성됩니다. 기본적으로 VM은 *Standard_DS1_v2* 크기에서 생성됩니다. 이 크기는 가용성 영역 미리 보기에서 지원됩니다.

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys --zone 1
```

VM을 만드는 데 몇 분이 걸릴 수 있습니다. VM이 만들어지면 Azure CLI에서 VM에 대한 정보를 출력합니다. VM이 실행되고 있는 가용성 영역을 나타내는 `zones` 값을 기록해 둡니다. 

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus2",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroupVM",
  "zones": "1"
}
```

## <a name="zone-for-ip-address-and-managed-disk"></a>IP 주소 및 관리 디스크에 대한 영역

가용성 영역에 VM을 배포하는 경우 IP 주소 및 관리 디스크 리소스는 동일한 가용성 영역에 배포됩니다. 다음 예에서는 이러한 리소스에 대한 정보를 가져옵니다.

먼저 [az vm list-ip-addresses](/cli/azure/vm#az_vm_list_ip_addresses) 명령을 사용하여 *myVM*에서 공용 IP 주소 리소스의 이름을 반환합니다. 이 예제에서는 이름이 변수에 저장되고 이후 단계에서 사용됩니다.

```azurecli-interactive
ipaddressname=$(az vm list-ip-addresses -g myResourceGroupVM -n myVM --query "[].virtualMachine.network.publicIpAddresses[].name" -o tsv)
```

이제 IP 주소에 대한 정보를 얻을 수 있습니다.

```azurecli-interactive
az network public-ip show --resource-group myResourceGroupVM --name $ipaddressname
```

IP 주소를 보여 주는 출력은 VM과 동일한 가용성 영역에 있습니다.

```azurecli-interactive
{
  "dnsSettings": null,
  "etag": "W/\"b7ad25eb-3191-4c8f-9cec-c5e4a3a37d35\"",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Network/publicIPAddresses/myVMPublicIP",
  "idleTimeoutInMinutes": 4,
  "ipAddress": "52.174.34.95",
  "ipConfiguration": {
    "etag": null,
    "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Network/networkInterfaces/myVMVMNic/ipConfigurations/ipconfigmyVM",
    "name": null,
    "privateIpAddress": null,
    "privateIpAllocationMethod": null,
    "provisioningState": null,
    "publicIpAddress": null,
    "resourceGroup": "myResourceGroupVM",
    "subnet": null
  },
  "location": "eastUS2",
  "name": "myVMPublicIP",
  "provisioningState": "Succeeded",
  "publicIpAddressVersion": "IPv4",
  "publicIpAllocationMethod": "Dynamic",
  "resourceGroup": "myResourceGroupVM",
  "resourceGuid": "8c70a073-09be-4504-0000-000000000000",
  "tags": {},
  "type": "Microsoft.Network/publicIPAddresses",
  "zones": [
    "1"
  ]
}
```

마찬가지로, VM의 관리 디스크가 가용성 영역에 있는지 확인합니다. [az vm show](/cli/azure/vm#az_vm_show) 명령을 사용하여 디스크 ID를 가져옵니다. 이 예제에서는 디스크 ID가 변수에 저장되고 이후 단계에서 사용됩니다. 

```azurecli-interactive
osdiskname=$(az vm show -g myResourceGroupVM -n myVM --query "storageProfile.osDisk.name" -o tsv)
```
이제 관리 디스크에 대한 정보를 얻을 수 있습니다.

```azurecli-interactive
az disk show --resource-group myResourceGroupVM --name $osdiskname
```

관리 디스크를 보여 주는 출력은 VM과 동일한 가용성 영역에 있습니다.

```azurecli-interactive
{
  "creationData": {
    "createOption": "FromImage",
    "imageReference": {
      "id": "/Subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/Providers/Microsoft.Compute/Locations/westeurope/Publishers/Canonical/ArtifactTypes/VMImage/Offers/UbuntuServer/Skus/16.04-LTS/Versions/latest",
      "lun": null
    },
    "sourceResourceId": null,
    "sourceUri": null,
    "storageAccountId": null
  },
  "diskSizeGb": 30,
  "encryptionSettings": null,
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/disks/osdisk_761c570dab",
  "location": "eastus2",
  "managedBy": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/myVM",
  "name": "osdisk_761c570dab",
  "osType": "Linux",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroupVM",
  "sku": {
    "name": "Premium_LRS",
    "tier": "Premium"
  },
  "tags": {},
  "timeCreated": "2017-09-05T22:16:06.892752+00:00",
  "type": "Microsoft.Compute/disks",
  "zones": [
    "1"
  ]
}
```
 


## <a name="next-steps"></a>다음 단계

이 문서에서는 가용성 영역에서 VM을 만드는 방법을 배웠습니다. Azure VM에 대한 [영역 및 가용성](regions-and-availability.md)에 대해 자세히 알아봅니다.




