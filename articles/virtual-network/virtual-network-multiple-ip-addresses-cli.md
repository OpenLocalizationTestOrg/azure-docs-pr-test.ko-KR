---
title: "hello Azure CLI 2.0을 사용 하 여 여러 IP 주소와 aaaVM | Microsoft Docs"
description: "여러 IP 해결 하는 tooassign 방법을 알아보려면 Azure CLI 2.0 hello tooa 가상 컴퓨터를 사용 하 여 | 리소스 관리자입니다."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 15efd853cc7c31bacb64ed052dabedd3fe4d3079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-cli-20"></a>Azure CLI 2.0 hello를 사용 하 여 toovirtual 컴퓨터에 여러 IP 주소 할당

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

이 문서에서는 toocreate hello Azure 리소스 관리자 배포 모델을 사용 하 여 가상 컴퓨터 (VM) Azure CLI 2.0 hello 하는 방법을 설명 합니다. Hello 클래식 배포 모델을 통해 만든 tooresources 여러 IP 주소를 할당할 수 없습니다. Azure 배포 모델을 읽을 hello에 대 한 자세한 toolearn [배포 모델을 이해](../resource-manager-deployment-model.md) 문서.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>여러 IP 주소를 사용하여 VM 만들기

Hello Azure CLI 2.0 (이 문서) 또는 hello를 사용 하 여이 작업을 완료할 수 있습니다 [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md)합니다. 사용자 환경에 적절 하 게 hello 값을 변경 합니다. 수행 하는 hello 단계 hello 시나리오에 설명 된 대로 toocreate 예로 여러 IP 사용 하 여 VM 해결 하는 방법을 설명 합니다. ""의 변수 값과 IP 주소 유형을 구현에 필요한 대로 변경합니다. 

1. Hello 설치 [Azure CLI 2.0](/cli/azure/install-az-cli2) 아직 없는 설치 하는 경우.
2. Hello의 hello 단계를 완료 하 여 Linux Vm에 대 한 SSH 공용 및 개인 키 쌍 만들기 [Linux Vm에 대 한 SSH 공용 및 개인 키 쌍 만들기](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.
3. Hello 명령 사용 하 여 로그인 명령 셸에서 `az login` 하 고 사용 중인 hello 구독을 선택 합니다.
4. Linux 또는 Mac 컴퓨터에서 다음에 나오는 hello 스크립트를 실행 하 여 hello VM을 만듭니다. hello 스크립트와 연결 된 Nic tooit hello 두 리소스 그룹, 하나의 가상 네트워크 (VNet), 세 가지 IP 구성 사용 하 여 NIC 1 개 및 VM을 만듭니다. hello NIC, 공용 IP 주소, 가상 네트워크 및 VM 리소스 모두에 존재 해야 hello 동일한 위치 및 구독 합니다. 하지만 hello 리소스 하지 않는 모든 tooexist에서 hello hello 그럴 스크립트 다음에 동일한 리소스 그룹입니다.

```bash
    
#!/bin/sh
    
RgName="myResourceGroup"
Location="westcentralus"
az group create --name $RgName --location $Location
    
# Create a public IP address resource with a static IP address using hello `--allocation-method Static` option. If you
# do not specify this option, hello address is allocated dynamically. hello address is assigned toohello resource from a pool
# of IP adresses unique tooeach Azure region. Download and view hello file from
# https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists hello ranges for each region.

PipName="myPublicIP"

# This name must be unique within an Azure location.
DnsName="myDNSName"

az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--dns-name $DnsName\
--allocation-method Static

# Create a virtual network with one subnet

VnetName="myVnet"
VnetPrefix="10.0.0.0/16"
VnetSubnetName="mySubnet"
VnetSubnetPrefix="10.0.0.0/24"

az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnetName \
--subnet-prefix $VnetSubnetPrefix

# Create a network interface connected toohello subnet and associate hello public IP address tooit. Azure will create the
# first IP configuration with a static private IP address and will associate hello public IP address resource tooit.

NicName="MyNic1"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--private-ip-address 10.0.0.4
--vnet-name $VnetName \
--public-ip-address $PipName
    
# Create a second public IP address, a second IP configuration, and associate it toohello NIC. This configuration has a
# static public IP address and a static private IP address.

az network public-ip create \
--resource-group $RgName \
--location $Location \
--name myPublicIP2 \
--dns-name mypublicdns2 \
--allocation-method Static

az network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--name IPConfig-2 \
--private-ip-address 10.0.0.5 \
--public-ip-name myPublicIP2

# Create a third IP configuration, and associate it toohello NIC. This configuration has  static private IP address and # no public IP address.

azure network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--private-ip-address 10.0.0.6 \
--name IPConfig-3

# Note: Though this article assigns all IP configurations tooa single NIC, you can also assign multiple IP configurations
# tooany NIC in a VM. toolearn how toocreate a VM with multiple NICs, read hello Create a VM with multiple NICs 
# article: https://docs.microsoft.com/azure/virtual-network/virtual-network-deploy-multinic-arm-cli.

# Create a VM and attach hello NIC.

VmName="myVm"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes rticle. hello script fails if hello VM size
# is not supported in hello location you select. Run hello `azure vm sizes --location estcentralus` command tooget a full list
# of VMs in US West Central, for example.

VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello utput returned by entering the
# `az vm image list` command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file. If you're creating a Windows VM, remove hello following
# line and you'll be prompted for hello password you want tooconfigure for hello VM.

SshKeyValue="~/.ssh/id_rsa.pub"

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $NicName \
--admin-username $Username \
--ssh-key-value $SshKeyValue
```

또한 3 개의 IP 구성이와 NIC 사용 하 여 VM toocreating hello 스크립트를 만듭니다.

- 단일 프리미엄 디스크를 기본적으로 관리 하지만 hello 디스크 유형 만들 수 있습니다에 대 한 다른 옵션이 있습니다. 읽기 hello [hello Azure CLI 2.0을 사용 하 여 Linux VM을 만들](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 을 참조 합니다.
- 하나의 서브넷 및 두 개의 공용 IP 주소를 가진 가상 네트워크. 또는 *기존* 가상 네트워크, 서브넷, NIC 또는 공용 IP 주소 리소스를 사용할 수 있습니다. 어떻게 toouse 기존 네트워크 리소스 대신 입력 추가 리소스를 만드는 toolearn `az vm create -h`합니다.

공용 IP 주소에는 명목 요금이 부과됩니다. 가격 책정, 주소 IP에 대 한 자세한 toolearn 읽을 hello [IP 주소 가격](https://azure.microsoft.com/pricing/details/ip-addresses) 페이지. 구독에서 사용할 수 있는 공용 IP 주소의 제한이 toohello 수가입니다. hello 제한, hello 읽기에 대 한 자세한 toolearn [Azure 제한](../azure-subscription-service-limits.md#networking-limits) 문서.

Hello VM을 만든 후 입력 hello `az network nic show --name MyNic1 --resource-group myResourceGroup` 명령 tooview hello NIC 구성 합니다. Hello 입력 `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` toohello NIC. tooview hello IP 구성의 목록에 연결

추가 hello 개인 IP 주소 수 toohello VM 운영 체제 hello에 운영 체제에 대 한 hello 단계를 완료 [추가 IP 주소 tooa VM 운영 체제](#os-config) 이 문서의 섹션.

## <a name="add"></a>IP 주소 tooa VM 추가

추가 개인 및 공용 IP 주소 tooan NIC를 수행 하는 hello 단계를 완료 하 여 기존를 추가할 수 있습니다. hello를 바탕으로 hello 예제 [시나리오](#Scenario) 이 문서에서 설명 합니다.

1. 단일 세션 내에서이 섹션의 단계를 남은 전체 hello 및 명령 셸을 엽니다. 전체 hello hello의 단계를 이미 설치 및 구성 하는 Azure CLI 없다면 [Azure CLI 2.0 설치](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) 아티클과 로그인 tooyour hello로 Azure 계정 `az-login` 명령입니다.

2. Hello 절, 요구 사항에 따라 다음 중 하나의 hello 단계를 완료 합니다.

    **개인 IP 주소 추가**
    
    개인 IP 주소 tooa NIC tooadd 뒤에 오는 hello 명령을 사용 하 여 IP 구성을 만들어야 합니다. hello 고정 IP 주소는 hello 서브넷에 대 한 사용 되지 않는 주소 여야 합니다.

    ```bash
    az network nic ip-config create \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --private-ip-address 10.0.0.7 \
    --name IPConfig-4
    ```
    
    고유한 구성 이름과 개인 IP 주소를 사용하여 필요한 만큼 구성을 만듭니다(정적 IP 주소를 가진 구성의 경우).

    **공용 IP 주소 추가**
    
    공용 IP 주소를 tooeither 연결 하 여 추가 되는 새 IP 구성 또는 기존 IP 구성 합니다. 필요한 만큼 따르려면 hello 섹션 중 하나에 hello 단계를 완료 합니다.

    공용 IP 주소에는 명목 요금이 부과됩니다. 가격 책정, 주소 IP에 대 한 자세한 toolearn 읽을 hello [IP 주소 가격](https://azure.microsoft.com/pricing/details/ip-addresses) 페이지. 구독에서 사용할 수 있는 공용 IP 주소의 제한이 toohello 수가입니다. hello 제한, hello 읽기에 대 한 자세한 toolearn [Azure 제한](../azure-subscription-service-limits.md#networking-limits) 문서.

    - **Hello 리소스 tooa 새 IP 구성에 연결**
    
        새 IP 구성의 공용 IP 주소를 추가할 때마다 모든 IP 구성 시 개인 IP 주소가 있어야 하기 때문에 개인 IP 주소도 추가해야 합니다. 기존 공용 IP 주소 리소스를 추가하거나 새로 만들 수 있습니다. toocreate 한 새 hello 다음 명령을 입력 합니다.
    
        ```bash
        az network public-ip create \
        --resource-group myResourceGroup \
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3
        ```

        개인 고정 IP 주소와 연결 된 hello 새 IP 구성이 toocreate *myPublicIP3* 공용 IP 리소스에 주소를 hello 다음 명령을 입력 합니다.

        ```bash
        az network nic ip-config create \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-5 \
        --private-ip-address 10.0.0.8
        --public-ip-address myPublicIP3
        ```

    - **연결 hello 리소스 tooan 기존 IP 구성** 공용 IP 주소 리소스에 아직 연결 되어 관련된 tooan IP 구성만 될 수 있습니다. IP 구성 hello 다음 명령을 입력 하 여 연결 된 공용 IP 주소에 있는지 여부를 확인할 수 있습니다.

        ```bash
        az network nic ip-config list \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --query "[?provisioningState=='Succeeded'].{ Name: name, PublicIpAddressId: publicIpAddress.id }" --output table
        ```

        반환되는 출력:
    
            Name        PublicIpAddressId
            
            ipconfig1   /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
            IPConfig-2  /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
            IPConfig-3

        Hello 이후 **PublicIpAddressId** 열에 대 한 *IpConfig-3* 는 hello 비어 출력을 공용 IP 주소 리소스가 현재 연결된 tooit 합니다. 기존 공용 IP 주소 리소스 tooIpConfig-3, 더하거나 명령 toocreate 하나를 수행 하는 hello 입력:

        ```bash
        az network public-ip create \
        --resource-group  myResourceGroup
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3 \
        --allocation-method Static
        ```
    
        다음 명령을 tooassociate hello 공용 IP 주소 리소스 toohello 기존 IP 구성 라는 hello 입력 *IPConfig-3*:
    
        ```bash
        az network nic ip-config update \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-3 \
        --public-ip myPublicIP3
        ```

3. 보기 hello 개인 IP 주소 및 공용 IP hello 다음 명령을 입력 하 여 NIC hello toohello 할당 된 리소스 Id를 처리 합니다.

    ```bash
    az network nic ip-config list \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --query "[?provisioningState=='Succeeded'].{ Name: name, PrivateIpAddress: privateIpAddress, PrivateIpAllocationMethod: privateIpAllocationMethod, PublicIpAddressId: publicIpAddress.id }" --output table
    ```

    반환되는 출력: <br>
    
        Name        PrivateIpAddress    PrivateIpAllocationMethod   PublicIpAddressId
        
        ipconfig1   10.0.0.4            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
        IPConfig-2  10.0.0.5            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
        IPConfig-3  10.0.0.6            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP3
    

4. Hello에 대 한 hello 지침에 따라 toohello NIC toohello VM 운영 체제를 추가한 hello 개인 IP 주소 추가 [추가 IP 주소 tooa VM 운영 체제](#os-config) 이 문서의 섹션. Hello 공용 IP 주소 toohello 운영 체제를 추가 하지 마십시오.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
