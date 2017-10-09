---
title: "i p v 6-Azure CLI aaaCreate 인터넷 연결 부하 분산 장치 | Microsoft Docs"
description: "Toocreate는 인터넷 연결 부하 분산 장치 i p v 6에 Azure 리소스 관리자를 사용 하 여 Azure CLI hello 하는 방법에 대해 알아봅니다"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "ipv6, Azure Load Balancer, 이중 스택, 공용 IP, 기본 ipv6, 모바일, iot"
ms.assetid: a1957c9c-9c1d-423e-9d5c-d71449bc1f37
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 7ff75ac90d74a74e3d0c27672b36fbd955a086a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-hello-azure-cli"></a>경우에 인터넷 연결 i p v 6에서 Azure 리소스 관리자 hello Azure CLI를 사용 하 여 부하 분산 장치 만들기

> [!div class="op_single_selector"]
> * [PowerShell](load-balancer-ipv6-internet-ps.md)
> * [Azure CLI](load-balancer-ipv6-internet-cli.md)
> * [템플릿](load-balancer-ipv6-internet-template.md)

Azure 부하 분산 장치는 계층 4(TCP, UDP) 부하 분산 장치입니다. hello 부하 분산 장치 부하 분산 장치 집합의 가상 컴퓨터 또는 클라우드 서비스의 비정상 상태 서비스 인스턴스 간에 들어오는 트래픽을 분산 하 여 고가용성을 제공 합니다. Azure Load Balancer는 여러 포트, 여러 IP 주소 또는 둘 다에서 이러한 서비스를 제공할 수도 있습니다.

## <a name="example-deployment-scenario"></a>예제 배포 시나리오

hello 다음 다이어그램에서는 hello 부하 분산 솔루션이이 문서에서 설명 하는 hello 예제 서식 파일을 사용 하 여 배포 되 고 있습니다.

![부하 분산 장치 시나리오](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

이 시나리오에서는 Azure 리소스를 수행 하는 hello를 만듭니다.

* 2개의 가상 컴퓨터(VM)
* 할당된 IPv4 및 IPv6 주소를 사용하는 각 VM에 대한 가상 네트워크 인터페이스
* IPv4 및 IPv6 공용 IP 주소를 가진 인터넷 연결 부하 분산 장치
* 가용성 집합 toothat hello 두 Vm이 포함
* 두 개의 끝점을 로드 균형 조정 규칙 toomap hello 공용 Vip toohello 개인

## <a name="deploying-hello-solution-using-hello-azure-cli"></a>Hello Azure CLI를 사용 하 여 hello 솔루션 배포

단계를 수행 하는 hello toocreate 인터넷 연결 부하 분산 장치 CLI Azure 리소스 관리자를 사용 하는 방법을 보여 줍니다. Azure 리소스 관리자와 각 리소스 만들어집니다 및 개별적으로 구성 된 한 다음 함께 toocreate 리소스.

부하 분산 장치 toodeploy 만들고 구성한 다음 개체는 hello:

* 프런트 엔드 IP 구성 - 들어오는 네트워크 트래픽에 대한 공용 IP 주소를 포함합니다.
* 백 엔드 주소 풀-hello hello 부하 분산 장치에서 가상 컴퓨터 tooreceive 네트워크 트래픽에 대 한 Nic (네트워크 인터페이스)를 포함 합니다.
* 부하 분산 규칙-hello 백 엔드 주소 풀의 부하 분산 장치 tooport hello에 공용 포트 매핑 규칙을 포함 합니다.
* 인바운드 NAT 규칙-hello hello 백 엔드 주소 풀에서 특정 가상 컴퓨터에 대 한 부하 분산 장치 tooa 포트에 공용 포트 매핑 규칙을 포함 합니다.
* 프로브-hello 백 엔드 주소 풀에 있는 가상 컴퓨터 인스턴스의 사용 된 검색 toocheck 가용성 상태를 포함 합니다.

자세한 내용은 [부하 분산 장치에 대한 Azure Resource Manager 지원](load-balancer-arm.md)을 참조하세요.

## <a name="set-up-your-cli-environment-toouse-azure-resource-manager"></a>CLI 환경 toouse Azure 리소스 관리자 설정

예를 들어 hello CLI 도구는 PowerShell 명령 창에서 실행 중인 합니다. Hello Azure PowerShell cmdlet를 사용 하지 않지만 PowerShell의 스크립팅 기능 tooimprove 가독성 및 재사용을 사용 합니다.

1. Azure CLI 처음 사용 하는 경우 참조 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) Azure 계정 및 구독을 선택 하면 toohello 포인트 hello 지침을 따릅니다.
2. Hello 실행 **azure 구성 모드** 명령 tooswitch tooResource 관리자 모드입니다.

    ```azurecli
    azure config mode arm
    ```

    예상 출력:

        info:    New mode is arm

3. TooAzure에 로그인 하 고 구독 목록을 가져옵니다.

    ```azurecli
    azure login
    ```

    메시지가 표시되면 Azure 자격 증명을 입력합니다.

    ```azurecli
    azure account list
    ```

    Toouse hello 구독을 선택 합니다. Hello 다음 단계에 대 한 hello 구독 Id 기록해 둡니다.

4. Hello CLI 명령과 함께 사용 하기 위해 PowerShell 변수를 설정 합니다.

    ```powershell
    $subscriptionid = "########-####-####-####-############"  # enter subscription id
    $location = "southcentralus"
    $rgName = "pscontosorg1southctrlus09152016"
    $vnetName = "contosoIPv4Vnet"
    $vnetPrefix = "10.0.0.0/16"
    $subnet1Name = "clicontosoIPv4Subnet1"
    $subnet1Prefix = "10.0.0.0/24"
    $subnet2Name = "clicontosoIPv4Subnet2"
    $subnet2Prefix = "10.0.1.0/24"
    $dnsLabel = "contoso09152016"
    $lbName = "myIPv4IPv6Lb"
    ```

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a>리소스 그룹, 부하 분산 장치, 가상 네트워크 및 서브넷 만들기

1. 리소스 그룹 만들기

    ```azurecli
    azure group create $rgName $location
    ```

2. 부하 분산 장치 만들기

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. VNet(가상 네트워크)를 만듭니다.

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    이 VNet에 두 개의 서브넷을 만듭니다.

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-hello-front-end-pool"></a>Hello 프런트 엔드 풀에 대 한 공용 IP 주소 만들기

1. Hello PowerShell 변수를 설정

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. 공용 IP 주소 hello 프런트 엔드 IP 풀을 만듭니다.

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > hello 부하 분산 장치는 FQDN으로 hello 공용 IP의 도메인 레이블을 hello를 사용합니다. 이 부하 분산 장치 FQDN hello으로 hello 클라우드 서비스 이름을 사용 하는 클래식 배포에서 변경 된 사항입니다.
    > 이 예제에서는 hello FQDN은 *contoso09152016.southcentralus.cloudapp.azure.com*합니다.

## <a name="create-front-end-and-back-end-pools"></a>프런트 엔드 및 백 엔드 풀 만들기

이 예제는 hello 프런트 엔드 풀에서 hello 부하 분산 된 네트워크 트래픽을 전송 하는 위치 hello 백 엔드 IP 풀과 hello hello 부하 분산 장치에서 들어오는 네트워크 트래픽을 수신 하는 hello 프런트 엔드 IP 풀을 만듭니다.

1. Hello PowerShell 변수를 설정

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. Hello 부하 분산 장치 및 hello 이전 단계에서 만든 hello 공용 IP를 연결 하는 프런트 엔드 IP 풀을 만듭니다.

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-hello-probe-nat-rules-and-lb-rules"></a>Hello 프로브, NAT 규칙 및 LB 규칙 만들기

이 예에서는 hello 다음 항목을 만듭니다.

* 연결 tooTCP 포트 80에 대 한 프로브 규칙 toocheck
* NAT 규칙 tootranslate 포트 3389 tooport 3389에 들어오는 모든 트래픽을 rdp<sup>1</sup>
* NAT 규칙 tootranslate 포트 3390 tooport 3389에 들어오는 모든 트래픽을 rdp<sup>1</sup>
* 부하 분산 장치 규칙 toobalance hello에 포트 80 tooport 80에 들어오는 모든 트래픽을 hello 백 엔드 풀에서 해결합니다.

<sup>1</sup> NAT 규칙은 hello 부하 분산 장치 뒤에 있는 특정 가상 컴퓨터 인스턴스 관련된 tooa 합니다. toohello 특정 가상 컴퓨터와 관련 된 hello NAT 규칙 포트 3389 포트에 도착 하는 hello 네트워크 트래픽이 전송 됩니다. NAT 규칙에 대한 프로토콜(UDP 또는 TCP)을 지정해야 합니다. 두 프로토콜을 모두 안 toohello 동일한 포트를 할당 합니다.

1. Hello PowerShell 변수를 설정

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. Hello 프로브 만들기

    hello 다음 예제에서는 연결 tooback 엔드 TCP 포트 80에 대 한 확인 하는 TCP 검색은 15 초 마다 두 개의 연속 된 실패 후 사용할 수 없는 hello 백 엔드 리소스로 표시 됩니다 것입니다.

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. Toohello 백 엔드 리소스 RDP 연결을 허용 하는 인바운드 NAT 규칙 만들기

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. 부하 분산 장치는 수신 하는 프런트 엔드 hello 요청에 따라 toodifferent 백 엔드 포트 트래픽을 전송 하는 규칙 만들기

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. 설정을 확인합니다.

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    예상 출력:

        info:    Executing command network lb show
        info:    Looking up hello load balancer "myIPv4IPv6Lb"
        data:    Id                              : /subscriptions/########-####-####-####-############/resourceGroups/pscontosorg1southctrlus09152016/providers/Microsoft.Network/loadBalancers/myIPv4IPv6Lb
        data:    Name                            : myIPv4IPv6Lb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : southcentralus
        data:    Provisioning state              : Succeeded
        data:
        data:    Frontend IP configurations:
        data:    Name             Provisioning state  Private IP allocation  Private IP   Subnet  Public IP
        data:    ---------------  ------------------  ---------------------  -----------  ------  ---------
        data:    FrontendVipIPv4  Succeeded           Dynamic                                     myIPv4Vip
        data:    FrontendVipIPv6  Succeeded           Dynamic                                     myIPv6Vip
        data:
        data:    Probes:
        data:    Name                 Provisioning state  Protocol  Port  Path  Interval  Count
        data:    -------------------  ------------------  --------  ----  ----  --------  -----
        data:    ProbeForIPv4AndIPv6  Succeeded           Tcp       80          15        2
        data:
        data:    Backend Address Pools:
        data:    Name             Provisioning state
        data:    ---------------  ------------------
        data:    BackendPoolIPv4  Succeeded
        data:    BackendPoolIPv6  Succeeded
        data:
        data:    Load Balancing Rules:
        data:    Name                  Provisioning state  Load distribution  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    --------------------  ------------------  -----------------  --------  -------------  ------------  ------------------  -----------------------
        data:    LBRuleForIPv4-Port80  Succeeded           Default            Tcp       80             80            false               4
        data:    LBRuleForIPv6-Port80  Succeeded           Default            Tcp       80             8080          false               4
        data:
        data:    Inbound NAT Rules:
        data:    Name                 Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    -------------------  ------------------  --------  -------------  ------------  ------------------  -----------------------
        data:    NatRule-For-Rdp-VM1  Succeeded           Tcp       3389           3389          false               4
        data:    NatRule-For-Rdp-VM2  Succeeded           Tcp       3391           3389          false               4
        info:    network lb show

## <a name="create-nics"></a>NIC 만들기

Nic를 만들고 tooNAT 규칙, 부하 분산 장치 규칙 및 프로브에 연결 합니다.

1. Hello PowerShell 변수를 설정

    ```powershell
    $nic1Name = "myIPv4IPv6Nic1"
    $nic2Name = "myIPv4IPv6Nic2"
    $subnet1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet1Name"
    $subnet2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet2Name"
    $backendAddressPoolV4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV4Name"
    $backendAddressPoolV6Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV6Name"
    $natRule1V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule1V4Name"
    $natRule2V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule2V4Name"
    ```

2. 각 백 엔드에 대한 NIC를 만들고 IPv6 구성을 추가합니다.

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-hello-back-end-vm-resources-and-attach-each-nic"></a>Hello 백 엔드 VM 리소스를 만들고 각 NIC 연결.

Vm toocreate 저장소 계정이 있어야 합니다. 부하 분산 hello Vm 가용성 집합의 toobe 멤버가 필요 합니다. VM 만들기에 대한 자세한 내용은 [PowerShell을 사용하여 Azure VM 만들기](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)

1. Hello PowerShell 변수를 설정

    ```powershell
    $storageAccountName = "ps08092016v6sa0"
    $availabilitySetName = "myIPv4IPv6AvailabilitySet"
    $vm1Name = "myIPv4IPv6VM1"
    $vm2Name = "myIPv4IPv6VM2"
    $nic1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic1Name"
    $nic2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic2Name"
    $disk1Name = "WindowsVMosDisk1"
    $disk2Name = "WindowsVMosDisk2"
    $osDisk1Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk1Name.vhd"
    $osDisk2Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk2Name.vhd"
    $imageurn "MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest"
    $vmUserName = "vmUser"
    $mySecurePassword = "PlainTextPassword*1"
    ```

    > [!WARNING]
    > 이 예제에서는 일반 텍스트로 hello Vm에 대 한 hello 사용자 이름 및 암호를 사용 합니다. 사용 하 여 선택을 취소 hello 자격 증명 하는 경우 적절 한 주의 해야 합니다. PowerShell에서 자격 증명을 처리 하는 보다 안전한 방법을, 참조 hello [Get-credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.

2. Hello 저장소 계정 및 가용성 집합 만들기

    Hello Vm을 만들 때 기존 저장소 계정을 사용할 수 있습니다. 다음 명령을 hello를 새 저장소 계정을 만듭니다.

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    다음으로 hello 가용성 집합을 만듭니다.

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. 연결 된 hello nic가 있는 hello 가상 컴퓨터 만들기

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a>다음 단계

[내부 부하 분산 장치 구성 시작](load-balancer-get-started-ilb-arm-cli.md)

[부하 분산 장치 배포 모드 구성](load-balancer-distribution-mode.md)

[부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성](load-balancer-tcp-idle-timeout.md)
