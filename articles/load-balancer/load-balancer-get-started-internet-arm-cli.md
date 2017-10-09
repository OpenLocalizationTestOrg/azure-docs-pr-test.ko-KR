---
title: "aaaCreate 인터넷 연결 부하 분산 장치-Azure CLI | Microsoft Docs"
description: "Toocreate는 인터넷 연결 부하 분산 장치에 리소스 관리자를 사용 하 여 Azure CLI hello 하는 방법에 대해 알아봅니다"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a8bcdd88-f94c-4537-8143-c710eaa86818
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: cadb5edb3b4a4e2f0813109d027eaafdc7ef7303
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-load-balancer-using-hello-azure-cli"></a>Hello Azure CLI를 사용 하 여 인터넷 부하 분산 장치 만들기

> [!div class="op_single_selector"]
> * [포털](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [템플릿](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

이 문서에서는 hello 리소스 관리자 배포 모델에 설명 합니다. 수도 있습니다 [toocreate 인터넷 연결 부하 분산 장치 클래식 배포를 사용 하는 방법에 대해 알아봅니다](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-using-hello-azure-cli"></a>Hello Azure CLI를 사용 하 여 hello 솔루션 배포

단계를 수행 하는 hello toocreate 인터넷 연결 부하 분산 장치 CLI Azure 리소스 관리자를 사용 하는 방법을 보여 줍니다. Azure 리소스 관리자와 각 리소스를 만들고 개별적으로 구성한 다음 준비 toocreate 리소스.

만들고 해야 개체 toodeploy 부하 분산 장치 뒤 hello 구성:

* 프런트 엔드 IP 구성 - 들어오는 네트워크 트래픽에 대한 공용 IP 주소를 포함합니다.
* 백 엔드 주소 풀-hello hello 부하 분산 장치에서 가상 컴퓨터 tooreceive 네트워크 트래픽에 대 한 Nic (네트워크 인터페이스)를 포함 합니다.
* 부하 분산 규칙-hello 백 엔드 주소 풀의 부하 분산 장치 tooport hello에 공용 포트 매핑 규칙을 포함 합니다.
* 인바운드 NAT 규칙-hello hello 백 엔드 주소 풀에서 특정 가상 컴퓨터에 대 한 부하 분산 장치 tooa 포트에 공용 포트 매핑 규칙을 포함 합니다.
* 프로브-hello 백 엔드 주소 풀에 있는 가상 컴퓨터 인스턴스의 사용 된 검색 toocheck 가용성 상태를 포함 합니다.

자세한 내용은 [부하 분산 장치에 대한 Azure Resource Manager 지원](load-balancer-arm.md)을 참조하세요.

## <a name="set-up-cli-toouse-resource-manager"></a>CLI toouse 리소스 관리자 설정

1. Azure CLI 처음 사용 하는 경우 참조 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) Azure 계정 및 구독을 선택 하면 toohello 포인트 hello 지침을 따릅니다.
2. Hello 실행 **azure 구성 모드** 명령 tooswitch tooResource 관리자 모드에서는 다음과 같이 합니다.

    ```azurecli
        azure config mode arm
    ```

    예상 출력:

        info:    New mode is arm

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a>가상 네트워크 및 hello 프런트 엔드 IP 풀에 대 한 공용 IP 주소 만들기

1. 명명 된 가상 네트워크 (VNet) 만들기 *NRPVnet* 라는 리소스 그룹을 사용 하 여 hello 미국 동부 위치에 *NRPRG*합니다.

    ```azurecli
        azure network vnet create NRPRG NRPVnet eastUS -a 10.0.0.0/16
    ```

    *NRPVnet*에서 10.0.0.0/24의 CIDR 블록으로 *NRPVnetSubnet*이라는 서브넷을 만듭니다.

    ```azurecli
        azure network vnet subnet create NRPRG NRPVnet NRPVnetSubnet -a 10.0.0.0/24
    ```

2. 명명 된 공용 IP 주소 만들기 *NRPPublicIP* toobe DNS 이름 사용 하 여 프런트 엔드 IP 풀에서 사용 하는 *loadbalancernrp.eastus.cloudapp.azure.com*. 아래 hello 명령을 hello 정적 할당 형식을 사용 하 고 4 분의 유휴 시간 제한입니다.

    ```azurecli
        azure network public-ip create -g NRPRG -n NRPPublicIP -l eastus -d loadbalancernrp -a static -i 4
    ```

   > [!IMPORTANT]
   > hello 부하 분산 장치는 FQDN으로 hello 공용 IP의 도메인 레이블을 hello를 사용 합니다. 이 부하 분산 장치 정규화 된 도메인 이름 (FQDN) hello으로 hello 클라우드 서비스를 사용 하는 클래식 배포에서 변경 된 사항입니다.
   > 이 예제에서는 hello FQDN은 *loadbalancernrp.eastus.cloudapp.azure.com*합니다.

## <a name="create-a-load-balancer"></a>부하 분산 장치 만들기

hello 다음 명령은 명명 된 부하 분산 장치 *NRPlb* hello에 *NRPRG* hello의 리소스 그룹 *미국 동부* 는 Azure 위치입니다.

    ```azurecli
    azure network lb create NRPRG NRPlb eastus
    ```

## <a name="create-a-front-end-ip-pool-and-a-backend-address-pool"></a>프런트 엔드 IP 풀 및 백 엔드 주소 풀 만들기
이 방법을 보여 주는이 예제 toocreate hello 프런트 엔드 IP 풀을 hello hello 들어오는 네트워크 트래픽을 받는 부하 분산 장치 백 엔드 IP 풀 hello 프런트 엔드 풀에서 hello 부하 분산 된 네트워크 트래픽을 전송 하는 위치를 hello 합니다.

1. Hello 부하 분산 장치 및 hello 이전 단계에서 만든 hello 공용 IP를 연결 하는 프런트 엔드 IP 풀을 만듭니다.

    ```azurecli
        azure network lb frontend-ip create nrpRG NRPlb NRPfrontendpool -i nrppublicip
    ```

2. Tooreceive 들어오는 트래픽을 hello 프런트 엔드 IP 풀에서 사용 하는 백 엔드 주소 풀을 설정 합니다.

    ```azurecli
        azure network lb address-pool create NRPRG NRPlb NRPbackendpool
    ```

## <a name="create-lb-rules-nat-rules-and-probe"></a>LB 규칙, NAT 규칙 및 프로브 만들기

이 예제는 hello 다음 항목을 만듭니다.

* NAT 규칙 tootranslate 포트 21 tooport 22에서 들어오는 모든 트래픽을<sup>1</sup>
* NAT 규칙 tootranslate 포트 23 tooport 22에서 들어오는 모든 트래픽을
* 부하 분산 장치 규칙 toobalance hello에 포트 80 tooport 80에 들어오는 모든 트래픽을 hello 백 엔드 풀에서 해결합니다.
* 명명 된 페이지에는 프로브 규칙 toocheck hello 상태 상태 *HealthProbe.aspx*합니다.

<sup>1</sup> NAT 규칙은 hello 부하 분산 장치 뒤에 있는 특정 가상 컴퓨터 인스턴스 관련된 tooa 합니다. 21 포트에 도착 하는 hello 네트워크 트래픽은 22이 NAT 규칙와 연결 된 포트에서 tooa 특정 가상 컴퓨터를 전송 됩니다. NAT 규칙에 대한 프로토콜(UDP 또는 TCP)을 지정해야 합니다. 두 프로토콜을 모두 안 toohello 동일한 포트를 할당 합니다.

1. Hello NAT 규칙을 만듭니다.

    ```azurecli
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh1 --protocol tcp --frontend-port 21 --backend-port 22
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh2 --protocol tcp --frontend-port 23 --backend-port 22
    ```

2. 부하 분산 장치를 만듭니다.

    ```azurecli
        azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name NRPfrontendpool --backend-address-pool-name NRPbackendpool
    ```

3. 상태 프로브를 만듭니다.

    ```azurecli
        azure network lb probe create --resource-group nrprg --lb-name nrplb --name healthprobe --protocol "http" --port 80 --path healthprobe.aspx --interval 15 --count 4
    ```

4. 설정을 확인합니다.

    ```azurecli
        azure network lb show nrprg nrplb
    ```

    예상 출력:

        info:    Executing command network lb show
        + Looking up hello load balancer "nrplb"
        + Looking up hello public ip "NRPPublicIP"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb
        data:    Name                            : nrplb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : eastus
        data:    Provisioning State              : Succeeded
        data:    Frontend IP configurations:
        data:      Name                          : NRPfrontendpool
        data:      Provisioning state            : Succeeded
        data:      Public IP address id          : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/publicIPAddresses/NRPPublicIP
        data:      Public IP allocation method   : Static
        data:      Public IP address             : 40.114.13.145
        data:
        data:    Backend address pools:
        data:      Name                          : NRPbackendpool
        data:      Provisioning state            : Succeeded
        data:
        data:    Load balancing rules:
        data:      Name                          : HTTP
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 80
        data:      Backend port                  : 80
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:      Backend address pool          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:
        data:    Inbound NAT rules:
        data:      Name                          : ssh1
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 21
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:      Name                          : ssh2
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 23
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:    Probes:
        data:      Name                          : healthprobe
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Http
        data:      Port                          : 80
        data:      Interval in seconds           : 15
        data:      Number of probes              : 4
        data:
        info:    network lb show command OK

## <a name="create-nics"></a>NIC 만들기

Toocreate nic가 필요 (또는 기존 템플릿을 수정할)와 tooNAT 규칙, 부하 분산 장치 규칙 및 프로브에 연결 합니다.

1. 명명 된 NIC를 만들고 *lb nic1 수*, hello와 연결 *rdp1* NAT 규칙을 hello *NRPbackendpool* 백 엔드 주소 풀입니다.

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" eastus
    ```

    예상 출력:

        info:    Executing command network nic create
        + Looking up hello network interface "lb-nic1-be"
        + Looking up hello subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up hello network interface "lb-nic1-be"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        data:    Name                            : lb-nic1-be
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : eastus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 10.0.0.4
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet
        data:      Load balancer backend address pools
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:      Load balancer inbound NAT rules:
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1
        data:
        info:    network nic create command OK

2. 명명 된 NIC를 만들고 *lb nic2 수*, hello와 연결 *rdp2* NAT 규칙을 hello *NRPbackendpool* 백 엔드 주소 풀입니다.

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" eastus
    ```

3. 라는 가상 컴퓨터 (VM) 만들기 *web1*, hello 라는 NIC에 연결할 *lb nic1 수*합니다. 저장소 계정 이라는 *web1nrp* 아래 hello 명령을 실행 하기 전에 생성 합니다.

    ```azurecli
        azure vm create --resource-group nrprg --name web1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

    > [!IMPORTANT]
    > Vm에서 부하 분산 장치 필요 toobe에 hello 동일한 가용성 집합입니다. 사용 하 여 `azure availset create` toocreate 한 가용성 집합입니다.

    hello 출력은 비슷한 toohello 다음 됩니다.

        info:    Executing command vm create
        + Looking up hello VM "web1"
        Enter username: azureuser
        Enter password for azureuser: *********
        Confirm password: *********
        info:    Using hello VM Size "Standard_A1"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account web1nrp
        + Looking up hello availability set "nrp-avset"
        info:    Found an Availability set "nrp-avset"
        + Looking up hello NIC "lb-nic1-be"
        info:    Found an existing NIC "lb-nic1-be"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet" in hello NIC "lb-nic1-be"
        info:    This is a NIC without publicIP configured
        + Creating VM "web1"
        info:    vm create command OK

    > [!NOTE]
    > hello 정보 메시지 **publicIP 구성 하지 않고 NIC 이것이** 만들어지므로 hello NIC tooInternet hello 부하 분산 장치 공용 IP 주소를 사용 하 여 연결 하는 hello 부하 분산 장치에 대 한 필요 합니다.

    Hello 이후 *lb nic1 수* hello와 연결 된 NIC *rdp1* NAT 규칙을 너무 연결할 수 있습니다*web1* 3441 hello 부하 분산 장치에 포트를 통해 RDP를 사용 합니다.

4. 라는 가상 컴퓨터 (VM) 만들기 *web2*, hello 라는 NIC에 연결할 *lb nic2 수*합니다. 저장소 계정 이라는 *web1nrp* 아래 hello 명령을 실행 하기 전에 생성 합니다.

    ```azurecli
        azure vm create --resource-group nrprg --name web2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="update-an-existing-load-balancer"></a>기존 부하 분산 장치 업데이트
기존 부하 분산 장치를 참조하는 규칙을 추가할 수 있습니다. Hello 다음 예제는 새 부하 분산 장치 규칙 tooan 기존 부하 분산 장치 추가 **NRPlb**

```azurecli
azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule2 --protocol tcp --frontend-port 8080 --backend-port 8051 --frontend-ip-name frontendnrppool --backend-address-pool-name NRPbackendpool
```

## <a name="delete-a-load-balancer"></a>부하 분산 장치 삭제
명령 tooremove 부하 분산 장치 뒤 hello를 사용 합니다.

```azurecli
azure network lb delete --resource-group nrprg --name nrplb
```

## <a name="next-steps"></a>다음 단계
[내부 부하 분산 장치 구성 시작](load-balancer-get-started-ilb-arm-cli.md)

[부하 분산 장치 배포 모드 구성](load-balancer-distribution-mode.md)

[부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성](load-balancer-tcp-idle-timeout.md)
