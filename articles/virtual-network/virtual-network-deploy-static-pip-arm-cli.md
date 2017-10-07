---
title: "고정 공용 IP 주소-Azure CLI 2.0을 사용 하 여 VM aaaCreate | Microsoft Docs"
description: "고정 공용 IP 주소를 사용 하 여 사용 하 여 VM toocreate Azure CLI (명령줄 인터페이스) 2.0 hello 하는 방법을 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 55bc21b0-2a45-4943-a5e7-8d785d0d015c
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486060463486462dd8336734a7ad23c4a2cba452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-cli-20"></a>고정 공용 IP 주소로 hello Azure CLI 2.0을 사용 하 여 VM 만들기

> [!div class="op_single_selector"]
> * [Azure 포털](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md)
> * [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md)
> * [템플릿](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell(클래식)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)이라는 두 가지 배포 모델이 있습니다. 이 문서에서는 Microsoft hello 클래식 배포 모델 대신 대부분의 새 배포에 권장 하는 hello 리소스 관리자 배포 모델을 사용 하 여 설명 합니다.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name = "create"></a>Hello VM 만들기

Hello Azure CLI 2.0 (이 문서) 또는 hello를 사용 하 여이 작업을 완료할 수 있습니다 [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md)합니다. hello에 값 "" 다음에 나오는 hello 단계의 hello 변수 hello 시나리오의 설정으로 리소스를 만듭니다. 사용자 환경에 적절 하 게 hello 값을 변경 합니다.

1. Hello 설치 [Azure CLI 2.0](/cli/azure/install-az-cli2) 아직 없는 설치 하는 경우.
2. Hello의 hello 단계를 완료 하 여 Linux Vm에 대 한 SSH 공용 및 개인 키 쌍 만들기 [Linux Vm에 대 한 SSH 공용 및 개인 키 쌍 만들기](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.
3. Hello 명령 사용 하 여 로그인 명령 셸에서 `az login`합니다.
4. Linux 또는 Mac 컴퓨터에서 다음에 나오는 hello 스크립트를 실행 하 여 hello VM을 만듭니다. Azure 공용 IP 주소, 가상 네트워크, 네트워크 인터페이스 hello 및 VM 리소스 모두에 존재 해야 hello 동일 위치 합니다. 하지만 hello 리소스 하지 않는 모든 tooexist에서 hello hello 그럴 스크립트 다음에 동일한 리소스 그룹입니다.

```bash
RgName="IaaSStory"
Location="westus"

# Create a resource group.

az group create \
--name $RgName \
--location $Location

# Create a public IP address resource with a static IP address using hello --allocation-method Static option.
# If you do not specify this option, hello address is allocated dynamically. hello address is assigned toothe
# resource from a pool of IP adresses unique tooeach Azure region. hello DnsName must be unique within the
# Azure location it's created in. Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653#
# that lists hello ranges for each region.

PipName="PIPWEB1"
DnsName="iaasstoryws1"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static \
--dns-name $DnsName

# Create a virtual network with one subnet

VnetName="TestVNet"
VnetPrefix="192.168.0.0/16"
SubnetName="FrontEnd"
SubnetPrefix="192.168.1.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $SubnetName \
--subnet-prefix $SubnetPrefix

# Create a network interface connected toohello VNet with a static private IP address and associate hello public IP address
# resource toohello NIC.

NicName="NICWEB1"
PrivateIpAddress="192.168.1.101"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $SubnetName \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress \
--public-ip-address $PipName

# Create a new VM with hello NIC

VmName="WEB1"

# Replace hello value for hello VmSize variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article.
VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable with a value for *urn* from hello output returned by entering
# hello `az vm image list` command. 

OsImage="credativ:Debian:8:latest"
Username='adminuser'

# Replace hello following value with hello path tooyour public key file.
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
# If creating a Windows VM, remove hello previous line and you'll be prompted for hello password you want tooconfigure for hello VM.
```

또한 VM toocreating hello 스크립트를 만듭니다.
- 단일 프리미엄 디스크를 기본적으로 관리 하지만 hello 디스크 유형 만들 수 있습니다에 대 한 다른 옵션이 있습니다. 읽기 hello [hello Azure CLI 2.0을 사용 하 여 Linux VM을 만들](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 을 참조 합니다.
- 가상 네트워크, 서브넷, NIC 및 공용 IP 주소 리소스입니다. 또는 *기존* 가상 네트워크, 서브넷, NIC 또는 공용 IP 주소 리소스를 사용할 수 있습니다. 어떻게 toouse 기존 네트워크 리소스 대신 입력 추가 리소스를 만드는 toolearn `az vm create -h`합니다.

## <a name = "validate"></a>VM 생성 및 공용 IP 주소의 유효성 검사

1. Hello 명령을 입력 `az resource list --resouce-group IaaSStory --output table` toosee hello 리소스 hello 스크립트로 만든 목록입니다. 출력을 반환 하는 hello에 5 개의 리소스 있어야: 네트워크 인터페이스, 디스크, 공용 IP 주소, 가상 네트워크 및 가상 컴퓨터.
2. Hello 명령을 입력 `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`합니다. 출력을 반환 하는 hello에서 hello 값을 기록해 둡니다 **IpAddress** 및 해당 hello 값 **PublicIpAllocationMethod** 은 *정적*합니다.
3. 다음 명령을 hello를 실행 하기 전에 제거 hello <>, 대체 *Username* hello에 사용한 hello 이름의 **사용자 이름** hello 스크립트 및 바꾸기에 변수 *ipAddress* hello로 **ipAddress** hello 이전 단계에서 합니다. 실행된 hello 다음 명령은 tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`합니다. 

## <a name= "clean-up"></a>Hello VM 및 관련된 리소스를 제거 합니다.

프로덕션 환경에서 사용 하지 않는 경우이 연습에서 만든 hello 리소스를 삭제 하는 것이 좋습니다. VM, 공용 IP 주소 및 디스크 리소스를 프로비전하는 경우 요금이 발생합니다. 이 연습에서는 전체 hello 단계를 수행 하는 동안 생성 된 tooremove hello 리소스:

1. hello 리소스 그룹에서 실행 hello tooview hello 리소스 `az resource list --resource-group IaaSStory` 명령입니다.
2. 이 문서의 hello 스크립트에 의해 생성 된 hello 리소스 이외의 hello 리소스 그룹에 리소스가 없는지 확인 합니다. 
3. 이 연습에서는 실행 hello에서에서 모든 리소스를 만들 toodelete `az group delete -n IaaSStory` 명령입니다. hello 명령은 hello 리소스 그룹 및 포함 된 모든 hello 리소스를 삭제 합니다.

## <a name="next-steps"></a>다음 단계

모든 네트워크 트래픽은 tooand VM이이 문서에서 만든 hello에서 전달 될 수 있습니다. Tooand hello 네트워크 인터페이스, hello 서브넷 또는 둘 다에서 전달할 수 있는 hello 트래픽을 제한 하는 NSG 내에서 인바운드 및 아웃 바운드 규칙을 정의할 수 있습니다. hello 읽을 Nsg에 대 한 자세한 toolearn [NSG 개요](virtual-networks-nsg.md) 문서.
