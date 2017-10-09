---
title: "네트워크 보안 그룹-aaaTroubleshoot PowerShell | Microsoft Docs"
description: "Azure PowerShell을 사용 하 여 hello Azure 리소스 관리자 배포에서 tootroubleshoot 네트워크 보안 그룹을 모델링 하는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 4c732bb7-5cb1-40af-9e6d-a2a307c2a9c4
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 95fd60fa72cf6d17fa990e3c3eb7d980878f7c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-azure-powershell"></a>Azure PowerShell을 사용하여 네트워크 보안 그룹 문제 해결
> [!div class="op_single_selector"]
> * [Azure 포털](virtual-network-nsg-troubleshoot-portal.md)
> * [PowerShell](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

가상 컴퓨터 (VM)에 (Nsg) 네트워크 보안 그룹을 구성 하 고 VM 연결 문제가 발생 하는 경우이 문서에서는 Nsg toohelp 추가 문제 해결에 대 한 진단 기능에 대 한 개요를 제공 합니다.

Nsg를 사용 하면 toocontrol hello 유형의 트래픽 가상 컴퓨터 (Vm) 및 해당 흐름 있습니다. Nsg에는 Azure 가상 네트워크 (VNet), 네트워크 인터페이스 (NIC), 또는 둘 다에 적용 된 toosubnets 될 수 있습니다. hello 효과적인 규칙이 적용 되는 tooa NIC hello 적용할 Nsg tooa NIC 및 hello 서브넷에 연결 되어 있는 hello 규칙의 집계 됩니다. 때로는 이러한 NSG 간의 규칙이 서로 충돌하고 VM의 네트워크 연결에 영향을 줄 수 있습니다.  

VM의 Nic에 적용 될 때 프로그램 Nsg에서 모든 hello 효과적인 보안 규칙을 볼 수 있습니다. 이 문서에서는 tootroubleshoot VM 연결 문제에 이러한 규칙을 사용 하 여 Azure 리소스 관리자 배포 모델을 hello 하는 방법을 보여 줍니다. VNet과 NSG 개념에 잘 모르겠으면 읽을 hello [가상 네트워크](virtual-networks-overview.md) 및 [네트워크 보안 그룹](virtual-networks-nsg.md) 개요 문서입니다.

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a>효과적인 보안 규칙 tootroubleshoot VM 트래픽 흐름을 사용 하 여
다음에 나오는 hello 시나리오는 일반적인 연결 문제의 예:

VM *VM1*은 *WestUS-VNet1*이라는 VNet 내에 있는 *Subnet1* 서브넷의 일부입니다. 시도 tooconnect toohello RDP를 사용 하 여 TCP 포트 3389 통해 VM에 실패 합니다. 두 hello NIC에 Nsg 적용 *VM1 NIC1* 서브넷 hello 및 *Subnet1*합니다. 트래픽 tooTCP 포트 3389는 hello hello 네트워크 인터페이스와 연결 된 NSG에에서 사용할 수 있습니다. *VM1 NIC1*TCP 포트 3389 실패 tooVM1의 ping 있지만, 합니다.

이 예에서는 TCP 포트 3389를 사용 하는 동안 다음 단계 hello 모든 포트를 통해 사용 되는 toodetermine 인바운드 및 아웃 바운드 연결 오류가 발생할 수 있습니다.

## <a name="detailed-troubleshooting-steps"></a>자세한 문제 해결 단계
Hello 단계 tootroubleshoot Nsg를 VM에 대해 다음을 완료 합니다.

1. Azure PowerShell 세션 및 로그인 tooAzure를 시작 합니다. Azure PowerShell을 사용 하 여 잘 모르는 경우 읽기 hello [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 문서.
2. 다음 명령을 tooreturn 모든 NSG 규칙은 tooa 라는 NIC에 적용 하는 hello 입력 *VM1 NIC1* hello 리소스 그룹에 *g 1*:
   
        Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > NIC의 hello 이름을 모르면 hello 명령 tooretrieve hello 이름이 리소스 그룹의 모든 Nic 다음을 입력 합니다. 
   > 
   > `Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name`
   > 
   > 
   
    hello 다음 텍스트는 hello에 대 한 반환 하는 hello 효과적인 규칙 출력의 샘플 *VM1 NIC1* NIC:
   
        NetworkSecurityGroup   : {
                                   "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/VM1-NIC1-NSG"
                                 }
        Association            : {
                                   "NetworkInterface": {
                                     "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkInterfaces/VM1-NIC1"
                                   }
                                 }
        EffectiveSecurityRules : [
                                 {
                                 "Name": "securityRules/allowRDP",
                                 "Protocol": "Tcp",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "3389-3389",
                                 "SourceAddressPrefix": "Internet",
                                 "DestinationAddressPrefix": "0.0.0.0/0",
                                 "ExpandedSourceAddressPrefix": [… ],
                                 "ExpandedDestinationAddressPrefix": [],
                                 "Access": "Allow",
                                 "Priority": 1000,
                                 "Direction": "Inbound"
                                 },
                                 {
                                 "Name": "defaultSecurityRules/AllowVnetInBound",
                                 "Protocol": "All",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "0-65535",
                                 "SourceAddressPrefix": "VirtualNetwork",
                                 "DestinationAddressPrefix": "VirtualNetwork",
                                 "ExpandedSourceAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                 "ExpandedDestinationAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                  "Access": "Allow",
                                  "Priority": 65000,
                                  "Direction": "Inbound"
                                  },…
                         ]
   
        NetworkSecurityGroup   : {
                                   "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/Subnet1-NSG"
                                 }
        Association            : {
                                   "Subnet": {
                                     "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/virtualNetworks/WestUS-VNet1/subnets/Subnet1"
                                 }
                                 }
        EffectiveSecurityRules : [
                                 {
                                "Name": "securityRules/denyRDP",
                                "Protocol": "Tcp",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "3389-3389",
                                "SourceAddressPrefix": "Internet",
                                "DestinationAddressPrefix": "0.0.0.0/0",
                                "ExpandedSourceAddressPrefix": [
                                   ... ],
                                "ExpandedDestinationAddressPrefix": [],
                                "Access": "Deny",
                                "Priority": 1000,
                                "Direction": "Inbound"
                                },
                                {
                                "Name": "defaultSecurityRules/AllowVnetInBound",
                                "Protocol": "All",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "0-65535",
                                "SourceAddressPrefix": "VirtualNetwork",
                                "DestinationAddressPrefix": "VirtualNetwork",
                                "ExpandedSourceAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "ExpandedDestinationAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "Access": "Allow",
                                "Priority": 65000,
                                "Direction": "Inbound"
                                },...
                                ]
   
    참고 hello 다음 hello 출력에 대 한 정보:
   
   * 서브넷과 연결된 섹션(*Subnet1*)과 NIC와 연결된 섹션(*VM1-NIC1*)의 두 **NetworkSecurityGroup** 섹션이 있습니다. 이 예제에서는 NSG tooeach 적용된 되었습니다.
   * **연결** 주어진된 NSG와 연결 된 hello 리소스 (서브넷 또는 NIC)를 보여 줍니다. 이면 hello NSG 리소스와 이동/분리이 명령을 실행 하기 전에 즉시 해야 toowait 몇 초 정도 hello 변경 tooreflect hello 명령 출력에 대 한 합니다. 
   * hello로 시작 하는 규칙 이름을 *defaultSecurityRules*: 때 NSG 만들어지고, 몇 가지 기본 보안 규칙에 만들어집니다. 기본 규칙은 제거할 수 없지만 더 높은 우선 순위 규칙으로 재정의할 수 있습니다.
     읽기 hello [NSG 개요](virtual-networks-nsg.md#default-rules) NSG에 대 한 자세한 문서 toolearn 기본 보안 규칙입니다.
   * **ExpandedAddressPrefix** NSG 기본 태그에 대 한 hello 주소 접두사를 확장 합니다. 태그는 여러 주소 접두사를 나타냅니다. Hello 태그 확장으로 /에서 특정 주소 접두사가 VM 연결 문제를 해결할 때 유용할 수 있습니다. 예를 들어 tooshow 확장 VIRTUAL_NETWORK 태그 VNET 피어 링와 겹치기 hello 이전 출력에 VNet 접두사입니다.
     
     > [!NOTE]
     > NSG를 서브넷, NIC의 경우, 또는 둘 다와 연결 된 경우 명령 표시 효과적인 규칙만 hello 합니다. 하나의 VM에 다른 NSG가 적용되는 여러 NIC가 있을 수 있습니다. 문제를 해결 하려면 각 NIC.에 대 한 hello 명령 실행
     > 
     > 
3. NSG 규칙 수가 많으면 통해 필터링 tooease hello 명령을 tootroubleshoot 추가로 다음을 입력 합니다. 
   
        $NSGs = Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
        $NSGs.EffectiveSecurityRules | Sort-Object Direction, Access, Priority | Out-GridView
   
    RDP 트래픽 (TCP 포트 3389)에 대 한 필터는 hello 다음 그림에에서 나와 있는 것 처럼 toohello 그리드 보기에 적용:
   
    ![규칙 목록](./media/virtual-network-nsg-troubleshoot-powershell/rules.png)
4. 둘 다 허용 및 거부 RDP에 대 한 규칙은 hello 그리드 보기에서 볼 수 있습니다, 합니다. hello 2 단계의 출력과 해당 hello *DenyRDP* hello toohello 서브넷 적용할 NSG 규칙이 설정 되어 있습니다. 인바운드 규칙에 대 한 적용 Nsg toohello 서브넷 먼저 처리 됩니다. 일치 하는 항목이 hello 적용할 NSG toohello 네트워크 인터페이스는 처리 되지 않습니다. 이 경우 hello *DenyRDP* hello 서브넷에서 규칙의 RDP toohello VM 차단 (**VM1**).
   
   > [!NOTE]
   > VM에는 여러 Nic 연결 된 tooit이 있을 수 있습니다. 각각 다른 서브넷에 연결 된 tooa 수도 있습니다. Hello 이전 단계에서 hello 명령이 NIC에 대해 실행 되는데, 되므로이 사용자가 지정한 tooensure hello NIC를 hello 연결 오류가 발생 하면 중요 합니다. 확실 하지 않은 경우에 각 연결 된 NIC toohello VM에 대해 hello 명령의 항상 실행할 수 있습니다.
   > 
   > 
5. 변경 hello v m 1에 tooRDP *거부 RDP (3389)* 너무 규칙*허용 RDP(3389)* hello에 **Subnet1 NSG** NSG 합니다. TCP 포트 3389는 VM의 RDP 연결 toohello 열거나 hello PsPing 도구를 사용 하 여 열려 있는지 확인 하십시오. 읽는 hello 여 PsPing에 대 한 자세히 알아볼 수 있습니다 [PsPing 다운로드 페이지](https://technet.microsoft.com/sysinternals/psping.aspx)
   
    다음 명령을 hello에서 hello 출력에 hello 정보를 사용 하 여 NSG에서 규칙을 제거 하거나 수 있습니다.
   
        Get-Help *-AzureRmNetworkSecurityRuleConfig

## <a name="considerations"></a>고려 사항
연결 문제를 해결 하는 경우 지점 뒤에 hello를 고려 합니다.

* 기본 NSG 규칙 hello에서의 인바운드 액세스를 차단 합니다 인터넷 및 허용 VNet 인바운드 트래픽을 합니다. 규칙은 명시적으로 추가 되어야 tooallow 인바운드 필요에 따라 인터넷을 통해 액세스 합니다.
* VM의 네트워크 연결 toofail 일으키는 NSG 보안 규칙이 없으면로 인해 hello 문제 수 있습니다.
  * Hello VM의 운영 체제 내에서 실행 되는 방화벽 소프트웨어
  * 가상 어플라이언스 또는 온-프레미스 트래픽에 대해 경로가 구성되었습니다. 인터넷 트래픽을 통해 강제 터널링 리디렉션된 tooon 프레미스 될 수 있습니다. Hello 인터넷 tooyour VM에서에서 RDP/SSH 연결 hello 온-프레미스 네트워크 하드웨어가이 트래픽을 처리 하는 방법에 따라이 설정을 사용 하 여 작동 하지 않을 수 있습니다. 읽기 hello [경로 문제 해결](virtual-network-routes-troubleshoot-powershell.md) 문서 toolearn에 방해가 될 수 있는 toodiagnose 경로 문제 hello와 통신 흐름을 방법 hello VM입니다. 
* 기본적으로 Vnet을 살펴본 있는 hello VIRTUAL_NETWORK 태그 겹치기 Vnet에 대 한 tooinclude 접두사를 자동으로 확장 됩니다. Hello에 이러한 접두사를 볼 수 있습니다 **ExpandedAddressPrefix** 목록, tootroubleshoot 연결 피어 링 하는 문제 관련된 tooVNet 합니다. 
* 효과적인 보안 규칙은 NSG 또는 관련 된 hello VM NIC 및 서브넷 있는지에 표시 됩니다. 
* Hello NIC와 관련 된 없는 Nsg 또는 서브넷 있는 경우 tooyour VM에 할당 된 공용 IP 주소 이면 모든 포트 인바운드 및 아웃 바운드 액세스를 위해 열린 됩니다. Hello VM에 공용 IP 주소, 서브넷 또는 NIC에 Nsg toohello 적용이 좋습니다.  

