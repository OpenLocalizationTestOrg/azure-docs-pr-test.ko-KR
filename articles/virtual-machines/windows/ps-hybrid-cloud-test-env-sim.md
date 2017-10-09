---
title: "aaaSimulated 하이브리드 클라우드 테스트 환경 | Microsoft Docs"
description: "Azure 가상 네트워크 두 개와 VNet 간 연결을 사용하여 IT 전문가 또는 개발 테스트용 시뮬레이션된 하이브리드 클라우드 환경을 만들어봅니다."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ca5bf294-8172-44a9-8fed-d6f38d345364
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: 6063022e373c2b3564e040c4fbee122e2438974b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-simulated-hybrid-cloud-environment-for-testing"></a>테스트용 시뮬레이션된 하이브리드 클라우드 환경 설정
이 문서에서는 두 개의 Azure 가상 네트워크를 사용하여 Microsoft Azure에서 시뮬레이션된 하이브리드 클라우드 환경을 만드는 과정을 안내합니다. 다음은 hello 결과 구성입니다.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

하이브리드 클라우드 프로덕션 환경을 시뮬레이션하고 다음으로 구성됩니다.

* Azure 가상 네트워크 (hello 테스트 랩 가상 네트워크)에서 호스팅되는 시뮬레이션 및 간소화 된 온-프레미스 네트워크입니다.
* Azure에서 호스트되는 시뮬레이션된 크로스-프레미스 가상 네트워크(TestVNET)
* Hello 두 가상 네트워크 간의 VNet 대 VNet 연결입니다.
* Hello TestVNET 가상 네트워크의 보조 도메인 컨트롤러입니다.

이 구성은 다음 작업을 수행할 수 있는 기초 및 일반적인 시작 지점을 제공합니다.

* 시뮬레이션된 하이브리드 클라우드 환경에서 응용 프로그램 개발 및 테스트
* 컴퓨터, hello 테스트 랩 가상 네트워크 내에서 일부 및 일부 hello TestVNET 가상 네트워크, toosimulate 하이브리드 클라우드 기반 IT 작업 내에서 테스트 구성을 생성 합니다.

이 하이브리드 클라우드 테스트 환경 구축 하는 4 개의 주요 단계 toosetting 가지가 있습니다.

1. Hello 테스트 랩 가상 네트워크를 구성 합니다.
2. Hello 크로스-프레미스 가상 네트워크를 만듭니다.
3. Hello VNet 대 VNet VPN 연결을 만듭니다.
4. DC2 구성 

이 구성에는 Azure 구독이 필요합니다. MSDN 또는 Visual Studio 구독이 있는 경우에는 [Visual Studio 구독자를 위한 월간 Azure 크레딧](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 참조하세요.

> [!NOTE]
> Azure의 가상 컴퓨터 및 가상 네트워크 게이트웨이는 실행 중인 동안 지속적인 비용이 부과됩니다. 이 비용은 MSDN 또는 유료 구독에 대해 청구됩니다. Azure VPN 게이트웨이는 두 개의 Azure 가상 컴퓨터 집합으로 구현됩니다. toominimize hello 비용 hello 테스트 환경을 만들고 필요한 테스트 및 데모를 최대한 빨리 수행 합니다.
> 
> 

## <a name="phase-1-configure-hello-testlab-virtual-network"></a>1 단계: hello 테스트 랩 가상 네트워크 구성
Hello 지침을 사용 하 여 hello에 [기본 구성 테스트 환경](https://technet.microsoft.com/library/mt771177.aspx) 항목 tooconfigure hello DC1, APP1 및 CLIENT1 컴퓨터에 hello 테스트 랩 라는 Azure 가상 네트워크입니다. 

다음으로 Azure PowerShell 프롬프트를 시작합니다.

> [!NOTE]
> 명령 관계 집합 추적 hello 1.0 이상 Azure PowerShell을 사용 합니다.
> 
> 

Tooyour 계정에 로그인 합니다.

    Login-AzureRMAccount

다음 명령을 hello를 사용 하 여 구독 이름을 가져옵니다.

    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName

Azure 구독을 설정합니다. 사용 하 여 hello 동일 사용 했는지 toobuild 기본 구성에 1 단계에서에서 구독 합니다. Hello < 및 > 문자를 포함 하는 hello 따옴표 안의 hello 올바른 이름으로 바꿉니다.

    $subscr="<subscription name>"
    Get-AzureRmSubscription –SubscriptionName $subscr | Select-AzureRmSubscription

다음을 게이트웨이 서브넷 toohello 테스트 랩 가상 네트워크를 사용 하는 toohost hello Azure 게이트웨이 수 있는 기본 구성에 추가 합니다.

    $rgName="<name of your resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $vnet=Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name TestLab
    Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 10.255.255.248/29 -VirtualNetwork $vnet
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet

다음으로 hello 테스트 랩 가상 네트워크에 대 한 공용 IP 주소 tooassign toohello 게이트웨이 요청 합니다.

    $gwpip=New-AzureRmPublicIpAddress -Name TestLab_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic

그런 다음 게이트웨이를 만듭니다.

    $vnet=Get-AzureRmVirtualNetwork -Name TestLab -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name TestLab_GWConfig -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id 
    New-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

20 분 또는 자세한 toocreate 새 게이트웨이 걸릴 수 있습니다 염두에서에 둬야 합니다.

Hello 로컬 컴퓨터에 Azure 포털에서에서 tooDC1 hello CORP\User1 자격 증명으로 연결 합니다. tooconfigure hello CORP 도메인 컴퓨터 및 사용자가 인증을 위해 자신의 로컬 도메인 컨트롤러를 사용할 수 있도록 이러한 명령을 실행 관리자 권한으로 Windows PowerShell 명령 프롬프트에서 d c 1에서.

    New-ADReplicationSite -Name "TestLab" 
    New-ADReplicationSite -Name "TestVNET"
    New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
    New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "TestVNET"

다음은 현재 구성입니다.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph1.png)

## <a name="phase-2-create-hello-testvnet-virtual-network"></a>2 단계: hello TestVNET 가상 네트워크 만들기
먼저 hello TestVNET 가상 네트워크를 만들고 네트워크 보안 그룹으로 보호 합니다.

    $rgName="<name of hello resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $locShortName="<Azure location name from $locName in all lowercase letters with spaces removed. Example:  westus>"
    $testSubnet=New-AzureRMVirtualNetworkSubnetConfig -Name "TestSubnet" -AddressPrefix 192.168.0.0/24
    $gatewaySubnet=New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 192.168.255.248/29
    New-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName -Location $locName -AddressPrefix 192.168.0.0/16 -Subnet $testSubnet,$gatewaySubnet –DNSServer 10.0.0.4
    $rule1=New-AzureRMNetworkSecurityRuleConfig -Name "RDPTraffic" -Description "Allow RDP tooall VMs on hello subnet" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 3389
    New-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName -Location $locShortName -SecurityRules $rule1
    $vnet=Get-AzureRMVirtualNetwork -ResourceGroupName $rgName -Name TestVNET
    $nsg=Get-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName
    Set-AzureRMVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet" -AddressPrefix 192.168.0.0/24 -NetworkSecurityGroup $nsg

다음으로, 요청 공용 IP 주소 toobe hello TestVNET 가상 네트워크에 대 한 toohello 게이트웨이 할당 하 고 게이트웨이 만듭니다.

    $gwpip=New-AzureRmPublicIpAddress -Name TestVNET_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $vnet=Get-AzureRmVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name "TestVNET_GWConfig" -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
    New-AzureRmVirtualNetworkGateway -Name "TestVNET_GW" -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

다음은 현재 구성입니다.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph2.png)

## <a name="phase-3-create-hello-vnet-to-vnet-connection"></a>3 단계: hello VNet 대 VNet 연결 만들기
먼저 네트워크 또는 보안 관리자에서 임의로 암호화된 강력한 32자의 미리 공유한 키를 얻습니다. 또는에서 hello 정보를 사용 하 여 [IPsec 미리 공유한 키에 대 한 임의 문자열 만들기](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) tooobtain 사전 공유 키.

다음으로 이러한 명령을 toocreate hello VNet 대 VNet VPN 연결을 사용, 일부 시간 toocomplete 걸릴 수 있습니다.

    $sharedKey="<pre-shared key value>"
    $gwTestLab=Get-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName
    $gwTestVNET=Get-AzureRmVirtualNetworkGateway -Name TestVNET_GW -ResourceGroupName $rgName
    New-AzureRmVirtualNetworkGatewayConnection -Name TestLab_to_TestVNET -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestLab -VirtualNetworkGateway2 $gwTestVNET -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey
    New-AzureRmVirtualNetworkGatewayConnection -Name TestVNET_to_TestLab -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestVNET -VirtualNetworkGateway2 $gwTestLab -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey

몇 분 후 hello 연결을 설정 해야 합니다.

다음은 현재 구성입니다.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph3.png)

## <a name="phase-4-configure-dc2"></a>4단계: DC2 구성
먼저 DC2에 가상 컴퓨터를 만듭니다. Hello Azure PowerShell 명령 프롬프트에서 로컬 컴퓨터에이 명령은 실행 합니다.

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<hello storage account name for hello base configuration>"
    $vnet=Get-AzureRMVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $pip=New-AzureRMPublicIpAddress -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -PrivateIpAddress 192.168.0.4
    $vm=New-AzureRMVMConfig -VMName DC2 -VMSize Standard_A1
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestVNET-ADDSDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name ADDS-Data -DiskSizeInGB 20 -VhdUri $vhdURI  -CreateOption empty
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for DC2."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName DC2 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name DC2-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

다음으로 hello Azure 포털에서에서 toohello 새 DC2 가상 컴퓨터를 연결 합니다.

다음으로 기본 연결을 테스트 하는 것에 대 한 Windows 방화벽 규칙 tooallow 트래픽을 구성 합니다. DC2의 관리자 수준 Windows PowerShell 명령 프롬프트에서 다음 명령을 실행합니다.

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc1.corp.contoso.com

IP 주소가 10.0.0.4에서 4 개의 성공 응답 hello ping 명령을 발생 해야 합니다. VNet 대 VNet 연결 hello 트래픽의 테스트입니다.

다음으로 hello 추가 hello 드라이브 문자 f: 새 볼륨으로 d c 2에서 추가 데이터 디스크.

1. Hello 왼쪽된 창에서 서버 관리자의을 클릭 **파일 및 저장소 서비스**, 클릭 하 고 **디스크**합니다.
2. Hello 내용 창의 hello **디스크** 그룹에서 클릭 **2 디스크** (hello로 **파티션** 도**알 수 없는**).
3. **작업**을 클릭한 후 **새 볼륨**을 클릭합니다.
4. Hello hello 새 볼륨 마법사의 페이지를 시작 하기 전에 클릭 **다음**합니다.
5. Hello 선택 hello 서버 및 디스크 페이지에서 클릭 **디스크 2**, 클릭 하 고 **다음**합니다. 메시지가 표시되면 **확인**을 클릭합니다.
6. Hello hello 볼륨 페이지의 hello 크기 지정, 클릭 **다음**합니다.
7. Hello 할당 tooa 드라이브 문자 또는 폴더 페이지를 클릭 **다음**합니다.
8. Hello 선택 파일 시스템 설정 페이지에서 클릭 **다음**합니다.
9. 선택 확인 페이지 hello 클릭 **만들기**합니다.
10. 완료되면 **닫기**를 클릭합니다.

다음으로 d c 2 hello corp.contoso.com 도메인에 대 한 복제본 도메인 컨트롤러로 구성 합니다. D c 2에서 hello Windows PowerShell 명령 프롬프트에서이 명령은 실행 합니다.

    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"

CORP\User1 암호 및 디렉터리 서비스 복원 모드 (DSRM) 암호와 toorestart d c 2 hello 메시지 표시 toosupply는 둘 다 합니다.

이제에 hello TestVNET 가상 네트워크 자체 DNS 서버 (DC2),이 DNS 서버 hello TestVNET 가상 네트워크 toouse 구성 해야 합니다.

1. Hello Azure 포털의 왼쪽 창 hello hello 가상 네트워크 아이콘을 클릭 한 다음 클릭 **TestVNET**합니다.
2. Hello에 **설정** 탭을 클릭 **DNS 서버**합니다.
3. **주 DNS 서버**, 형식 **192.168.0.4** tooreplace 10.0.0.4입니다.
4. **Save**를 클릭합니다.

다음은 현재 구성입니다. 

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

이제 시뮬레이션된 하이브리드 클라우드 환경을 테스트할 준비가 완료되었습니다.

## <a name="next-step"></a>다음 단계
* 이 환경에서 [웹 기반 LOB(기간 업무) 응용 프로그램](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 설정합니다.

