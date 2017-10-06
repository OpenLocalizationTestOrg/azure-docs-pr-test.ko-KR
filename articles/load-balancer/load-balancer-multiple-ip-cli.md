---
title: "Azure CLI를 사용 하 여 여러 IP 구성에서 분산 aaaLoad | Microsoft Docs"
description: "여러 IP 해결 하는 tooassign 방법을 알아보려면 Azure CLI를 사용 하 여 tooa 가상 컴퓨터 | 리소스 관리자입니다."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: annahar
ms.openlocfilehash: df81e1b8193f274bad435d6b506c7be824117416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations"></a>여러 IP 구성의 부하 분산

> [!div class="op_single_selector"]
> * [포털](load-balancer-multiple-ip.md)
> * [CLI](load-balancer-multiple-ip-cli.md)
> * [PowerShell](load-balancer-multiple-ip-powershell.md)

이 문서에서는 Azure 부하 분산 장치에서 여러 ip toouse 보조 네트워크 인터페이스 (NIC)에서 해결 하는 방법을 설명 합니다. 이 시나리오에는 Windows를 실행하는 VM이 둘 있고 각각 기본 및 보조 NIC가 있습니다. 각 보조 hello Nic가 두 개의 IP 구성 합니다. 각 VM은 contoso.com 및 fabrikam.com 웹 사이트를 둘 다 호스트합니다. 각 웹 사이트는 hello 보조 NIC에서 hello IP 구성의 바인딩된 tooone Azure 부하 분산 장치 tooexpose 두 개의 프런트 엔드 IP 주소를 각 웹 사이트에 hello 웹 사이트에 대 한 toodistribute 트래픽 toohello 각 IP 구성에 대 한 사용 합니다. 이 시나리오에서는으로 백 엔드 풀 IP 주소 모두 같은 포트 번호 hello 합니다.

![LB 시나리오 이미지](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a>여러 IP 구성에 대 한 단계 tooload 잔액

이 문서에 설명 된 tooachieve hello 시나리오 아래 hello 단계를 수행 합니다.

1. [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) Azure 계정에 연결 된 문서 hello와 로그에 hello 단계에 따라 Azure CLI hello 합니다.
2. 위의 설명에 따라 *contosofabrikam*이라는 [리소스 그룹을 만듭니다](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group).

    ```azurecli
    azure group create contosofabrikam westcentralus
    ```

3. [가용성 집합 만들기](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) toofor hello 두 개의 Vm입니다. 이 시나리오에 대 한 hello 다음 명령을 사용 합니다.

    ```azurecli
    azure availset create --resource-group contosofabrikam --location westcentralus --name myAvailabilitySet
    ```

4. *myVNet*이라는 [가상 네트워크를 만들고](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) *mySubnet*이라는 서브넷을 만듭니다.

    ```azurecli
    azure network vnet create --resource-group contosofabrikam --name myVnet --address-prefixes 10.0.0.0/16  --location westcentralus

    azure network vnet subnet create --resource-group contosofabrikam --vnet-name myVnet --name mySubnet --address-prefix 10.0.0.0/24
    ```

5. [Hello 부하 분산 장치 만들기](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 호출 *mylb*:

    ```azurecli
    azure network lb create --resource-group contosofabrikam --location westcentralus --name mylb
    ```

6. 동적 부하 분산 장치의 프런트 엔드 IP 구성 hello에 대 한 공용 두 IP 주소를 만듭니다.

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp1 --domain-name-label contoso --allocation-method Dynamic

    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp2 --domain-name-label fabrikam --allocation-method Dynamic
    ```

7. Hello 두 프런트 엔드 IP 구성을 만들 *contosofe* 및 *fabrikamfe* 각각:

    ```azurecli
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp1 --name contosofe
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp2 --name fabrkamfe
    ```

8. *contosopool* 및 *fabrikampool*이라는 백 엔드 주소 풀과 [프로브](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP*를 만들고, *HTTPc* 및 *HTTPf*라는 부하 분산 규칙을 만듭니다.

    ```azurecli
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name contosopool
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name fabrikampool

    azure network lb probe create --resource-group contosofabrikam --lb-name mylb --name HTTP --protocol "http" --interval 15 --count 2 --path index.html

    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPc --protocol tcp --probe-name http--frontend-port 5000 --backend-port 5000 --frontend-ip-name contosofe --backend-address-pool-name contosopool
    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPf --protocol tcp --probe-name http --frontend-port 5000 --backend-port 5000 --frontend-ip-name fabrkamfe --backend-address-pool-name fabrikampool
    ```

9. 실행된 hello 다음 아래 명령을 클릭 한 다음 hello 출력을 너무 확인[부하 분산 장치 확인](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 올바로 생성 되었는지:

    ```azurecli
    azure network lb show --resource-group contosofabrikam --name mylb
    ```

10. 아래와 같이 VM1이라는 첫 번째 가상 컴퓨터에 대해 *myPublicIp*라는 [공용 IP를 만들고](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *mystorageaccont1*이라는 [저장소 계정을 만듭니다](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json).

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP --domain-name-label mypublicdns345 --allocation-method Dynamic

    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount1
    ```

11. [Hello 네트워크 인터페이스를 만들](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) v m 1에 대 한 두 번째 IP 구성을 추가 하 고 *VM1 ipconfig2*, 및 [hello VM을 만들](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) 아래와 같이:

    ```azurecli
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic1 --ip-config-name NIC1-ipconfig1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic2 --ip-config-name VM1-ipconfig1 --public-ip-name myPublicIP --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM1Nic2 --name VM1-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM1 --location westcentralus --os-type linux --nic-names VM1Nic1,VM1Nic2  --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount1 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

12. 두 번째 VM에 대해 10 ~ 11단계를 반복합니다.

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP2 --domain-name-label mypublicdns785 --allocation-method Dynamic
    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount2
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic2 --ip-config-name VM2-ipconfig1 --public-ip-name myPublicIP2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM2Nic2 --name VM2-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM2 --location westcentralus --os-type linux --nic-names VM2Nic1,VM2Nic2 --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount2 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

13. 마지막으로 DNS 리소스 레코드 toopoint toohello 각 프런트 엔드 IP 주소를 hello 부하 분산 장치를 구성 해야 합니다. 도메인을 Azure DNS에 호스트할 수 있습니다. Load Balancer와 Azure DNS를 사용하는 방법에 대한 자세한 내용은 [다른 Azure 서비스와 함께 Azure DNS 사용](../dns/dns-for-azure-services.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계
- 에 Azure에서 서비스 toocombine 부하 분산 방법에 대 한 자세한 [부하 분산 서비스를 사용 하 여 Azure에서](../traffic-manager/traffic-manager-load-balancing-azure.md)합니다.
- 다른 유형의 로그를 사용 하 여 Azure toomanage에 부하 분산 장치에 문제를 해결 하는 방법에 대해 알아봅니다 [Azure 부하 분산 장치에 대 한 로그 분석](../load-balancer/load-balancer-monitor-log.md)합니다.
