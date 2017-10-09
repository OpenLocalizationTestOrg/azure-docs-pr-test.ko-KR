---
title: "여러 Nic-Azure CLI 2.0을 사용 하 여 VM aaaCreate | Microsoft Docs"
description: "사용 하 여 여러 Nic 사용 하 여 VM toocreate Azure CLI 2.0 hello 하는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac0291a978e2c8682c69104915196cc6c4fcf8dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-20"></a>Hello Azure CLI 2.0을 사용 하 여 여러 Nic를 포함 한 VM 만들기

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.  사용 하 여이 문서에서는 Microsoft hello 대신 대부분의 새 배포에 권장 하는 hello 리소스 관리자 배포 모델 [클래식 배포 모델](virtual-network-deploy-multinic-classic-cli.md)합니다.
>

## <a name="create"></a>Hello VM 만들기

Hello Azure CLI 2.0 (이 문서) 또는 hello를 사용 하 여이 작업을 완료할 수 있습니다 [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md)합니다. hello에 값 "" 다음에 나오는 hello 단계의 hello 변수 hello 시나리오의 설정으로 리소스를 만듭니다. 사용자 환경에 적절 하 게 hello 값을 변경 합니다.

1. Hello 설치 [Azure CLI 2.0](/cli/azure/install-az-cli2) 아직 없는 설치 하는 경우.
2. Hello의 hello 단계를 완료 하 여 Linux Vm에 대 한 SSH 공용 및 개인 키 쌍 만들기 [Linux Vm에 대 한 SSH 공용 및 개인 키 쌍 만들기](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.
3. Hello 명령 사용 하 여 로그인 명령 셸에서 `az login`합니다.
4. Linux 또는 Mac 컴퓨터에서 다음에 나오는 hello 스크립트를 실행 하 여 hello VM을 만듭니다. hello 스크립트 리소스 그룹을 만듭니다 hello 두 Nic 사용 하 여 VM 서브넷 2 개, 두 개의 Nic와 하나의 가상 네트워크 (VNet) tooit 연결 합니다. Hello Nic 중 하나는 연결 된 tooone 서브넷 및 정적 공용 및 개인 IP 주소가 할당 됩니다. hello 다른 NIC는 연결 된 toohello 다른 서브넷 및 정적 개인 IP 주소와 공용 IP 주소 할당 됩니다. hello NIC, 공용 IP 주소, 가상 네트워크 및 VM 리소스 모두에 존재 해야 hello 동일한 위치 및 구독 합니다. 하지만 hello 리소스 하지 않는 모든 tooexist에서 hello hello 그럴 스크립트 다음에 동일한 리소스 그룹입니다.

```bash
#!/bin/sh

RgName="Multi-NIC-VM"
Location="westus"

# Create a resource group.
az group create \
--name $RgName \
--location $Location

# hello address is assigned toohello resource from a pool of IP adresses unique tooeach Azure region. 
# Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists
# hello ranges for each region.

PipName="PIP-WEB"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static

# Create a virtual network with one subnet

VnetName="VNet1"
VnetPrefix="10.0.0.0/16"
VnetSubnet1Name="Front-End"
VnetSubnet1Prefix="10.0.0.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnet1Name \
--subnet-prefix $VnetSubnet1Prefix

# Create a second subnet within hello VNet

VnetSubnet2Name="Back-end"
VnetSubnet2Prefix="10.0.1.0/24"
az network vnet subnet create \
--vnet-name $VnetName \
--resource-group $RgName \
--name $VnetSubnet2Name \
--address-prefix $VnetSubnet2Prefix

# Create a network interface connected tooone of hello subnets. hello NIC is assigned a single dynamic private and
# public IP address by default, but you can instead, assign static addresses, or no public IP address at all.
# You can also assign multiple private or public IP addresses tooeach NIC. toolearn more about IP addressing
# options for NICs, enter hello az network nic create -h command.

Nic1Name="NIC-FE"
PrivateIpAddress1="10.0.0.5"

az network nic create \
--name $Nic1Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress1 \
--public-ip-address $PipName

# Create a second network interface and connect it toohello other subnet. Though multiple NICs attached toohello same
# VM can be connected toodifferent subnets, hello subnets must all be within hello same VNet. Add additional NICs as necessary.

Nic2Name="NIC-BE"
PrivateIpAddress2="10.0.1.5"

az network nic create \
--name $Nic2Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet2Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress2

# Create a VM and attach hello two NICs.

VmName="WEB"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article. Not all VM sizes support
# more than one NIC, so be sure tooselect a VM size that supports hello number of NICs you want tooattach toohello VM.
# You must create hello VM with at least two NICs if you want tooadd more after VM creation. If you create a VM with
# only one NIC, you can't add additional NICs toohello VM after VM creation, regardless of how many NICs hello VM supports.
# hello VM size specified in hello following variable supports two NICs.

VmSize="Standard_DS2"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello output returned by entering the
# az vm image list command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file.

SshKeyValue="~/.ssh/id_rsa.pub"

# Before executing hello following command, add variable names of additional NICs you may have added toohello script that
# you want tooattach toohello VM. If creating a Windows VM, remove hello **ssh-key-value** line and you'll be prompted for
# hello password you want tooconfigure for hello VM.

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $Nic1Name $Nic2Name \
--admin-username $Username \
--ssh-key-value $SshKeyValue
```

또한 두 개의 Nic 사용 하 여 VM toocreating hello 스크립트를 만듭니다.
- 단일 프리미엄 디스크를 기본적으로 관리 하지만 hello 디스크 유형 만들 수 있습니다에 대 한 다른 옵션이 있습니다. 읽기 hello [hello Azure CLI 2.0을 사용 하 여 Linux VM을 만들](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 을 참조 합니다.
- 두 개의 서브넷 및 하나의 공용 IP 주소를 가진 가상 네트워크입니다. 또는 *기존* 가상 네트워크, 서브넷, NIC 또는 공용 IP 주소 리소스를 사용할 수 있습니다. 어떻게 toouse 기존 네트워크 리소스 대신 입력 추가 리소스를 만드는 toolearn `az vm create -h`합니다.

## <a name = "validate"></a>VM 생성 및 NIC 유효성 검사

1. Hello 명령을 입력 `az resource list --resouce-group Multi-NIC-VM --output table` toosee hello 리소스 hello 스크립트로 만든 목록입니다. 출력을 반환 하는 hello에 6 개의 리소스 있어야: 두 개의 Nic, 하나의 디스크, 하나의 공용 IP 주소, 하나의 가상 네트워크 및 가상 컴퓨터.
2. Hello 명령을 입력 `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`합니다. 출력을 반환 하는 hello에서 hello 값을 기록해 둡니다 **IpAddress** 및 해당 hello 값 **PublicIpAllocationMethod** 은 *정적*합니다.
3. 다음 명령을 hello를 실행 하기 전에 제거 hello <>, 대체 *Username* hello에 사용한 hello 이름의 **Username** hello 스크립트 및 바꾸기에 변수 *ipAddress* hello로 **ipAddress** hello 이전 단계에서 합니다. 실행된 hello 다음 명령은 tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`합니다. 
4. Toohello VM 연결 되 면 실행 hello `sudo ifconfig` 명령 toosee *eth0* 및 *e t h 1* 인터페이스입니다. 각 NIC hello 정적 개인 IP 주소는 hello Azure DHCP 서버 hello 스크립트에 지정 된 할당 되었습니다. hello toohello Nic를 할당 하는 IP 및 MAC 주소가 변경 되지 않습니다까지 hello VM이 삭제 됩니다. 변경 하지 않는 IP 주소는 운영 체제 내에서 지정 toohello 컴퓨터 연결을 해제할 수으로 하는 것이 좋습니다. 공용 IP 주소 네트워크 주소 변환 tooand hello hello Azure 인프라에서 개인 IP 주소에서 멤버인 hello 운영 체제 내에서 표시 되지 않습니다.

## <a name= "clean-up"></a>Hello VM 및 관련된 리소스를 제거 합니다.

프로덕션 환경에서 사용 하지 않는 경우이 연습에서 만든 hello 리소스를 삭제 하는 것이 좋습니다. VM, 공용 IP 주소 및 디스크 리소스를 프로비전하는 경우 요금이 발생합니다. 이 연습에서는 전체 hello 단계를 수행 하는 동안 생성 된 tooremove hello 리소스:
1. hello 리소스 그룹에서 실행 hello tooview hello 리소스 `az resource list --resource-group Multi-NIC-VM` 명령입니다.
2. 이 문서의 hello 스크립트에 의해 생성 된 hello 리소스 이외의 hello 리소스 그룹에 리소스가 없는지 확인 합니다. 
3. 이 연습에서는 실행 hello에서에서 모든 리소스를 만들 toodelete `az group delete --name Multi-NIC-VM` 명령입니다. hello 명령은 hello 리소스 그룹 및 포함 된 모든 hello 리소스를 삭제 합니다.

## <a name="next-steps"></a>다음 단계

모든 네트워크 트래픽은 tooand VM이이 문서에서 만든 hello에서 전달 될 수 있습니다. 각 네트워크 인터페이스, 각 서브넷 또는 둘 다에서 tooand 전달할 수 있는 hello 트래픽을 제한 하는 NSG 내에서 인바운드 및 아웃 바운드 규칙을 정의할 수 있습니다. hello 읽을 Nsg에 대 한 자세한 toolearn [NSG 개요](virtual-networks-nsg.md) 문서.
