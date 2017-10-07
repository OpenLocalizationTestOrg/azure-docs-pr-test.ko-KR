---
title: "aaaCreate는 내부 부하 분산 장치-Azure CLI | Microsoft Docs"
description: "Toocreate는 내부 부하 분산 장치를 사용 하 여 리소스 관리자의 Azure CLI hello 하는 방법에 대해 알아봅니다"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c7a24e92-b4da-43c0-90f2-841c1b7ce489
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3aea6fdb07600f0d661ec6b8ffc784b03380a127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-by-using-hello-azure-cli"></a>내부 부하 분산 장치는 hello Azure CLI를 사용 하 여 만들기

> [!div class="op_single_selector"]
> * [Azure 포털](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [템플릿](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.  사용 하 여이 문서에서는 Microsoft hello 대신 대부분의 새 배포에 권장 하는 hello 리소스 관리자 배포 모델 [클래식 배포 모델](load-balancer-get-started-ilb-classic-cli.md)합니다.

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-solution-by-using-hello-azure-cli"></a>Hello Azure CLI를 사용 하 여 hello 솔루션 배포

단계를 수행 하는 hello 어떻게 toocreate 인터넷 연결 부하 분산 장치 CLI와 Azure 리소스 관리자를 사용 하 여 보여 줍니다. Azure 리소스 관리자와 각 리소스 만들어집니다 및 개별적으로 구성 된 한 다음 함께 toocreate 리소스.

Toocreate 필요 하 고이 정보를 개체 toodeploy 부하 분산 장치 뒤 hello를 구성 합니다.

* **프런트 엔드 IP 구성**: 들어오는 네트워크 트래픽에 대한 공용 IP 주소를 포함합니다.
* **백 엔드 주소 풀**: hello hello 부하 분산 장치에서 가상 컴퓨터 tooreceive 네트워크 트래픽을 허용 하는 네트워크 인터페이스 (Nic)를 포함 합니다.
* **부하 분산 규칙**: hello 백 엔드 주소 풀의 부하 분산 장치 tooport hello에 공용 포트를 매핑하는 규칙이 포함
* **인바운드 NAT 규칙**: hello hello 백 엔드 주소 풀에서 특정 가상 컴퓨터에 대 한 부하 분산 장치 tooa 포트에 공용 포트를 매핑하는 규칙이 포함
* **프로브**: hello 백 엔드 주소 풀에 있는 가상 컴퓨터 인스턴스의 사용 되는 toocheck hello 가용성은 상태 프로브를 포함 합니다.

자세한 내용은 [부하 분산 장치에 대한 Azure Resource Manager 지원](load-balancer-arm.md)을 참조하세요.

## <a name="set-up-cli-toouse-resource-manager"></a>CLI toouse 리소스 관리자 설정

1. Azure CLI 처음 사용 하는 경우 참조 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md)합니다. Azure 계정 및 구독을 선택 하면 toohello 포인트 hello 지침을 따릅니다.
2. Hello 실행 **azure 구성 모드** tooswitch tooResource 관리자 모드를 다음과 같이 명령:

    ```azurecli
    azure config mode arm
    ```

    예상 출력:

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a>내부 부하 분산 장치를 단계별로 만듭니다.

1. TooAzure에 로그인 합니다.

    ```azurecli
    azure login
    ```

    메시지가 표시되면 Azure 자격 증명을 입력합니다.

2. Hello 명령 도구 tooAzure 리소스 관리자 모드를 변경 합니다.

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a>리소스 그룹 만들기

Azure Resource Manager의 모든 리소스는 리소스 그룹과 연결됩니다. 리소스 그룹을 아직 만들지 않았으면 만들도록 합니다.

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a>내부 부하 분산 장치 집합을 만듭니다.

1. 내부 부하 분산 장치 만들기

    시나리오를 따르는 hello, nrprg 라는 리소스 그룹은 미국 동부 지역에 생성 됩니다.

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > 동일한 리소스 그룹 hello 및 동일한 hello 같은 가상 네트워크 및 가상 네트워크 서브넷은 내부 부하 분산 장치에 대 한 모든 리소스에 있어야 영역입니다.

2. Hello 내부 부하 분산 장치에 대 한 프런트 엔드 IP 주소를 만듭니다.

    가상 네트워크의 hello 서브넷 범위에 사용 하는 hello IP 주소 여야 합니다.

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. Hello 백 엔드 주소 풀을 만듭니다.

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    프런트 엔드 IP 주소 및 백 엔드 주소 풀을 정의한 후에 부하 분산 장치 규칙, 인바운드 NAT 규칙을 만들고 상태 프로브를 사용자 지정할 수 있습니다.

4. Hello 내부 부하 분산 장치에 대 한 부하 분산 장치 규칙을 만듭니다.

    Hello 이전 단계를 수행 하는 경우 hello 명령은 설정 수신 tooport 1433에 대 한 부하 분산 장치 규칙 hello 프런트 엔드 풀 및 보내는 네트워크 부하 분산 된 트래픽 toohello 백 엔드 주소 풀에도 포트 1433을 사용 합니다.

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. 인바운드 NAT 규칙을 만듭니다.

    인바운드 NAT 규칙은 tooa 특정 가상 컴퓨터 인스턴스를 이동 하는 부하 분산 장치에 사용 되는 toocreate 끝점입니다. hello 이전 단계에는 원격 데스크톱에 대 한 NAT 규칙을 두 개 만들어집니다.

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. Hello 부하 분산 장치에 대 한 상태 프로브를 만듭니다.

    상태 검색에는 모든 가상 컴퓨터 인스턴스 toomake 네트워크 트래픽을 보낼 수 있는지 확인 합니다. 실패 한 프로브 검사를 사용 하 여 hello 가상 컴퓨터 인스턴스는 다시 온라인 상태로 전환 되 고 프로브 확인 정상 임을 확인 될 때까지 hello 부하 분산 장치에서 제거 됩니다.

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > hello Microsoft Azure 플랫폼에는 다양 한 관리 시나리오에 대 한 정적, 공개적으로 라우팅 가능한 IPv4 주소를 사용합니다. hello IP 주소 168.63.129.16입니다. 이 IP 주소를 방화벽으로 차단하면 안 됩니다. 예기치 않은 동작이 발생할 수 있습니다.
    > 존중 tooAzure 내부 부하 분산 가상 컴퓨터 부하 분산 집합에 대해 프로브 hello 부하 분산 장치 toodetermine hello 성능 상태를 모니터링 하 여이 IP 주소를 사용 합니다. 네트워크 보안 그룹 사용 되는 toorestrict 내부적으로 부하 분산 된 집합에 트래픽을 tooAzure 가상 컴퓨터는 되거나 적용 된 tooa 가상 네트워크 서브넷에 경우에 네트워크 보안 규칙 tooallow 트래픽을 168.63.129.16에서 추가 되어 있는지 확인 합니다.

## <a name="create-nics"></a>NIC 만들기

Toocreate nic가 필요 (또는 기존 템플릿을 수정할)와 tooNAT 규칙, 부하 분산 장치 규칙 및 프로브에 연결 합니다.

1. 명명 된 NIC를 만들 *lb nic1 수*, hello와 연결할 및 *rdp1* NAT 규칙 및 hello *beilb* 백 엔드 주소 풀입니다.

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
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

2. 명명 된 NIC를 만들 *lb nic2 수*, hello와 연결할 및 *rdp2* NAT 규칙 및 hello *beilb* 백 엔드 주소 풀입니다.

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. 라는 가상 컴퓨터 만들기 *DB1*, hello 라는 NIC와 연결할 및 *lb nic1 수*합니다. 저장소 계정 이라는 *web1nrp* hello 다음 명령을 실행 하기 전에 만들어집니다.

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > Vm에서 부하 분산 장치 필요 toobe에 hello 동일한 가용성 집합입니다. 사용 하 여 `azure availset create` toocreate 한 가용성 집합입니다.

4. 라는 가상 컴퓨터 (VM) 만들기 *DB2*, hello 라는 NIC와 연결할 및 *lb nic2 수*합니다. 저장소 계정 이라는 *web1nrp* hello 다음 명령을 실행 하기 전에 생성 합니다.

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a>부하 분산 장치 삭제

부하 분산 장치를 tooremove hello 다음 명령을 사용 합니다.

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a>다음 단계

[원본 IP 선호도를 사용하여 부하 분산 장치 배포 모드 구성](load-balancer-distribution-mode.md)

[부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성](load-balancer-tcp-idle-timeout.md)

