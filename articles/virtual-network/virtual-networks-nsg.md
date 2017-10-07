---
title: "Azure의 보안 그룹 aaaNetwork | Microsoft Docs"
description: "네트워크 보안 그룹을 사용 하 여 Azure에 배포 된 hello 방화벽을 사용 하 여 가상 네트워크 내에서 tooisolate 및 제어 트래픽 흐름이 하는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 20e850fc-6456-4b5f-9a3f-a8379b052bc9
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: jdial
ms.openlocfilehash: 3528ce833dab17977327c3c9ae0e78316e5e6a05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="filter-network-traffic-with-network-security-groups"></a>네트워크 보안 그룹을 사용하여 네트워크 트래픽 필터링

네트워크 보안 그룹 NSG ()를 허용 하거나 거부할 네트워크 트래픽 tooresources tooAzure 가상 네트워크 (VNet) 연결 하는 보안 규칙 목록이 포함 되어 있습니다. 개별 네트워크 인터페이스 (NIC) 연결 tooVMs (리소스 관리자) 또는 Nsg 연결된 toosubnets, 개별 Vm (클래식)를 수 있습니다. NSG 연결된 tooa 서브넷 이면 tooall 리소스 연결 된 toohello 서브넷 hello 규칙에 적용 됩니다. 또한 VM 또는 NIC.는 NSG tooa를 연결 하 여 트래픽을 추가로 제한할 수

> [!NOTE]
> Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다. 이 문서에서는 두 모델을 사용 하 여 있지만 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.

## <a name="nsg-resource"></a>NSG 리소스
Nsg에는 다음과 같은 속성 hello 포함 되어 있습니다.

| 속성 | 설명 | 제약 조건 | 고려 사항 |
| --- | --- | --- | --- |
| 이름 |NSG hello에 대 한 이름 |Hello 지역 내에서 고유 해야 합니다.<br/>문자, 숫자, 밑줄, 마침표 및 하이픈을 포함할 수 있습니다.<br/>문자 또는 숫자로 시작해야 합니다.<br/>문자, 숫자 또는 밑줄로 끝나야 합니다.<br/>80자를 초과할 수 없습니다. |여러 Nsg toocreate를 할 수 있습니다, 때문에 Nsg의 쉽게 tooidentify hello 기능을 게 한다는 명명 규칙이 있는지 확인 합니다. |
| 지역 |Azure [지역](https://azure.microsoft.com/regions) hello NSG를 만들 위치입니다. |Nsg hello 내에서 관련된 tooresources 수 NSG hello와 동일한 영역입니다. |hello를 읽기 지역당, 있어야 수 toolearn 개수 Nsg에 대 한 [Azure 제한](../azure-subscription-service-limits.md#virtual-networking-limits-classic) 문서.|
| 리소스 그룹 |hello [리소스 그룹](../azure-resource-manager/resource-group-overview.md#resource-groups) hello NSG에 존재 합니다. |NSG에는 리소스 그룹에 없는 수 있습니다 모든 리소스 그룹에 연결 된 tooresources hello 리소스 hello의 일부인으로 NSG hello와 같은 Azure 지역입니다. |리소스 그룹에 리소스가 사용 되는 toomanage 여러 개 배포 단위로 함께 합니다.<br/>Hello NSG를 연결 하는 리소스와 그룹화를 고려할 수 있습니다. |
| 규칙 |허용되거나 거부되는 트래픽을 정의하는 인바운드 또는 아웃바운드 규칙 | |Hello 참조 [NSG 규칙](#Nsg-rules) 이 문서의 섹션. |

> [!NOTE]
> 끝점 기반 Acl 및 네트워크 보안 그룹에서 지원 되지 않습니다 hello 동일한 VM 인스턴스. Toouse NSG를 원하는 위치에 끝점 ACL을 이미 있는 경우 먼저 hello 끝점 ACL을 제거 합니다. tooremove ACL을 읽는 방법 toolearn hello [관리 액세스 제어 목록 (Acl) PowerShell을 사용 하 여 끝점에 대 한](virtual-networks-acl-powershell.md) 문서.
> 

### <a name="nsg-rules"></a>NSG 규칙
NSG 규칙 hello 다음 속성이 포함 되어 있습니다.

| 속성 | 설명 | 제약 조건 | 고려 사항 |
| --- | --- | --- | --- |
| **Name** |Hello 규칙에 대 한 이름입니다. |Hello 지역 내에서 고유 해야 합니다.<br/>문자, 숫자, 밑줄, 마침표 및 하이픈을 포함할 수 있습니다.<br/>문자 또는 숫자로 시작해야 합니다.<br/>문자, 숫자 또는 밑줄로 끝나야 합니다.<br/>80자를 초과할 수 없습니다. |NSG 내에 여러 규칙을 규칙의 tooidentify hello 함수를 허용 하는 명명 규칙을 따르는 있는지 확인 될 수 있습니다. |
| **프로토콜** |Hello 규칙에 대 한 프로토콜 toomatch 합니다. |TCP, UDP, 또는 * |사용 하 여 * ICMP (동-서 트래픽에만 해당), 포함 되는 프로토콜으로, UDP 및 TCP와 마찬가지로 hello 해야 하는 규칙 수를 줄일 수 있습니다.<br/>At hello 동일한 시간을 사용 하 여 * 수 너무 광범위 한 접근 방식을 있으므로 사용 하는 것이 좋습니다. * 필요한 경우에 합니다. |
| **원본 포트 범위** |Hello 규칙에 대 한 원본 포트 범위 toomatch 합니다. |단일 1 too65535, 포트 범위에서에서 포트 번호 (예: 1-65535), 또는 * (모든 포트)에 대 한 합니다. |원본 포트는 사용 후 삭제될 수 있습니다. 클라이언트 프로그램에서 특정 포트를 사용하지 않는 한 대부분의 경우 "*"를 사용합니다.<br/>여러 규칙에 대 한 가능한 tooavoid hello 필요한 만큼 toouse 포트 범위를 시도 합니다.<br/>여러 포트 또는 포트 범위는 쉼표로 그룹화할 수 없습니다. |
| **대상 포트 범위** |Hello 규칙에 대 한 대상 포트 범위 toomatch 합니다. |단일 1 too65535, 포트 범위에서에서 포트 번호 (예: 1-65535), 또는 \* (모든 포트)에 대 한 합니다. |여러 규칙에 대 한 가능한 tooavoid hello 필요한 만큼 toouse 포트 범위를 시도 합니다.<br/>여러 포트 또는 포트 범위는 쉼표로 그룹화할 수 없습니다. |
| **원본 주소 접두사** |소스 주소 접두사 또는 태그 toomatch hello 규칙에 대 한 합니다. |단일 IP 주소(예: 10.10.10.10), IP 서브넷(예: 192.168.1.0/24), [기본 태그](#default-tags) 또는 *(모든 주소의 경우) |범위, 기본 태그를 사용 하는 것이 좋습니다 및 * 규칙 tooreduce hello 수 있습니다. |
| **대상 주소 접두사** |대상 주소 접두사 또는 태그 toomatch hello 규칙에 대 한 합니다. | 단일 IP 주소(예: 10.10.10.10), IP 서브넷(예: 192.168.1.0/24), [기본 태그](#default-tags) 또는 *(모든 주소의 경우) |범위, 기본 태그를 사용 하는 것이 좋습니다 및 * 규칙 tooreduce hello 수 있습니다. |
| **방향** |Hello 규칙에 대 한 트래픽 toomatch의 방향입니다. |인바운드 또는 아웃바운드 |인바운드 규칙과 아웃바운드 규칙은 방향에 따라 개별적으로 처리됩니다. |
| **우선 순위** |우선 순위에 따라 hello 규칙이 확인 됩니다. 규칙이 적용되면 일치하는 규칙은 더 이상 테스트되지 않습니다. | 100~4096 사이의 숫자 | 만들 수 있습니다 hello 이후 100이 새 규칙에 대 한 각 규칙 tooleave 공간에 대 한 우선 순위를 점프 규칙을 만드는 것이 좋습니다. |
| **Access** |액세스 tooapply hello 규칙과 일치 하는 경우의 형식입니다. | 허용 또는 거부 | 패킷을 허용 규칙 없으면 hello 패킷은 삭제 됩니다 염두에서에 둬야 합니다. |

NSG에는 두 가지 규칙 집합, 즉 인바운드 및 아웃바운드가 포함됩니다. hello 우선 순위 규칙에 대 한 각 집합 내에서 고유 해야 합니다. 

![NSG 규칙 처리](./media/virtual-network-nsg-overview/figure3.png) 

이전 그림 hello NSG 규칙이 처리 되는 방법을 보여 줍니다.

### <a name="default-tags"></a>기본 태그
기본 태그는 시스템 제공 식별자 tooaddress의 IP 주소 범주입니다. 기본 태그를 사용 하 여 hello에 **소스 주소 접두사** 및 **대상 주소 접두사** 모든 규칙의 속성입니다. 다음 3개의 기본 태그를 사용할 수 있습니다.

* **VirtualNetwork** (리소스 관리자) (**VIRTUAL_NETWORK** 기본에 대 한):이 태그 포함 hello 가상 네트워크 주소 공간 (CIDR 범위를 Azure에 정의 되어 있는 경우), 모든 온-프레미스 주소 공간을 연결 되 고 연결 Azure Vnet (로컬 네트워크)입니다.
* **AZURE_LOADBALANCER**(Resource Manager) (클래식의 경우 **AzureLoadBalancer**): 이 태그는 Azure의 인프라 부하 분산 장치를 나타내며, hello 태그 tooan 발생 하는 Azure의 상태를 조사 하는 Azure 데이터 센터 IP로 변환 합니다.
* **인터넷** (리소스 관리자) (**인터넷** 기본에 대 한):이 태그는 hello hello 가상 네트워크 외부 및 공용 인터넷에서 연결할 수 있는 IP 주소 공간을 나타냅니다. hello 범위 포함 hello [Azure 공용 IP 공간 소유](https://www.microsoft.com/download/details.aspx?id=41653)합니다.

### <a name="default-rules"></a>기본 규칙
모든 NSG에는 기본 규칙 집합이 포함됩니다. hello 기본 규칙은 삭제할 수 있지만 여 hello 만드는 규칙을 재정의할 수 hello 가장 낮은 우선 순위를 할당 되었으므로 있습니다. 

hello 기본 규칙에는 다음과 같이 트래픽을 허용 안 함 및 허용:
- **가상 네트워크:** 가상 네트워크에서 시작하고 끝나는 트래픽은 인바운드와 아웃바운드 방향 둘 다에서 허용됩니다.
- **인터넷:** 아웃바운드 트래픽은 허용되지만 인바운드 트래픽은 차단됩니다.
- **부하 분산 장치:** 의 Vm 및 역할 인스턴스 수 있도록 Azure의 부하 분산 장치 tooprobe hello 상태입니다. 부하 분산된 집합을 사용하지 않는 경우 이 규칙을 무시할 수 있습니다.

**인바운드 기본 규칙**

| Name | 우선 순위 | 원본 IP | 원본 포트 | 대상 IP | 대상 포트 | 프로토콜 | Access |
| --- | --- | --- | --- | --- | --- | --- | --- |
| AllowVNetInBound |65000 | VirtualNetwork | * | VirtualNetwork | * | * | 허용 |
| AllowAzureLoadBalancerInBound | 65001 | AzureLoadBalancer | * | * | * | * | 허용 |
| DenyAllInBound |65500 | * | * | * | * | * | 거부 |

**아웃바운드 기본 규칙**

| Name | 우선 순위 | 원본 IP | 원본 포트 | 대상 IP | 대상 포트 | 프로토콜 | Access |
| --- | --- | --- | --- | --- | --- | --- | --- |
| AllowVnetOutBound | 65000 | VirtualNetwork | * | VirtualNetwork | * | * | 허용 |
| AllowInternetOutBound | 65001 | * | * | 인터넷 | * | * | 허용 |
| DenyAllOutBound | 65500 | * | * | * | * | * | 거부 |

## <a name="associating-nsgs"></a>NSG 연결
NSG tooVMs, Nic 및 서브넷을 다음과 같이 사용 중인 hello 배포 모델에 따라 연결할 수 있습니다.

* **VM (기본에만 해당):** 보안 규칙이 적용 됩니다 tooall 트래픽을/hello VM에서에서 합니다. 
* **NIC (리소스 관리자에만 해당):** 보안 규칙이 적용 됩니다 tooall 트래픽을/hello NIC hello NSG에서에서에 연결 되어 있습니다. 다중 NIC VM에서 있습니다 수 다른 적용 (또는 동일한 hello) NSG tooeach NIC 개별적으로 합니다. 
* **(리소스 관리자 및 기본) 서브넷:** 보안 규칙이 적용 됩니다 tooany 트래픽을/리소스에서 toohello VNet를 연결 합니다.

다른 Nsg tooa VM (또는 NIC hello 배포 모델에 따라 다름)를 연결 하 고 hello NIC 또는 VM에 연결 되어 있는 서브넷 수 있습니다. 보안 규칙는 적용 된 toohello 트래픽 hello에 각 NSG의 우선 순위에 따라 다음과 같습니다. 순서:

- **인바운드 트래픽**

  1. **NSG 적용 toosubnet:** 서브넷 NSG가 일치 하는 규칙 toodeny 트래픽 hello 패킷은 삭제 됩니다.

  2. **NSG 적용 tooNIC** (리소스 관리자) 또는 VM (클래식): 경우 VM\NIC NSG에 트래픽을 거부 하는 일치 하는 규칙이, 서브넷 NSG에는 일치 하는 규칙이 트래픽을 허용 하는 경우에 hello VM\NIC, 패킷은 삭제 됩니다.

- **아웃바운드 트래픽**

  1. **NSG 적용 tooNIC** (리소스 관리자) 또는 VM (클래식): VM\NIC NSG 트래픽을 거부 하는 일치 하는 규칙이 있으면 패킷이 삭제 됩니다.

  2. **NSG 적용 toosubnet:** 서브넷 NSG 트래픽을 거부 하는 일치 하는 규칙이 있으면 패킷이 삭제 될 경우에 VM\NIC NSG가 트래픽을 허용 하는 일치 하는 규칙입니다.

> [!NOTE]
> 단일 NSG tooa 서브넷, VM 또는 NIC;만 연결할 수 있지만 연결할 수 있습니다 원하는 만큼 많은 리소스 동일한 NSG tooas hello 합니다.
>

## <a name="implementation"></a>구현
리소스 관리자 hello 또는 hello 다음 도구를 사용 하 여 클래식 배포 모델에서 Nsg를 구현할 수 있습니다.

| 배포 도구 | 클래식 | 리소스 관리자 |
| --- | --- | --- |
| Azure Portal   | 예 | [예](virtual-networks-create-nsg-arm-pportal.md) |
| PowerShell     | [예](virtual-networks-create-nsg-classic-ps.md) | [예](virtual-networks-create-nsg-arm-ps.md) |
| Azure CLI **V1**   | [예](virtual-networks-create-nsg-classic-cli.md) | [예](virtual-networks-create-nsg-cli-nodejs.md) |
| Azure CLI **V2**   | 아니요 | [예](virtual-networks-create-nsg-arm-cli.md) |
| Azure Resource Manager 템플릿   | 아니요  | [예](virtual-networks-create-nsg-arm-template.md) |

## <a name="planning"></a>계획
Nsg를 구현 하기 전에 다음 질문 tooanswer hello가 필요 합니다.

1. 어떤 유형의 리소스에서 toofilter 트래픽 tooor 할까요? NIC(Resource Manager), VM(클래식), Cloud Services, Application Service Environments 및 VM Scale Sets와 같은 리소스를 연결할 수 있습니다. 
2. 리소스가 hello toofilter 트래픽이 기존 Vnet에 연결 된 toosubnets에서 원하는?

Azure에서 네트워크 보안에 대 한 자세한 내용은 hello 읽을 [클라우드 서비스 및 네트워크 보안](../best-practices-network-security.md) 문서. 

## <a name="design-considerations"></a>디자인 고려 사항
Hello에 toohello 질문 hello 답변을 알고 있다면 [계획](#Planning) 섹션를 hello 여 Nsg를 정의 하기 전에 다음 섹션을 검토 합니다.

### <a name="limits"></a>제한
제한은 당 NSG 규칙의 수와 toohello 수 Nsg는 구독에 있을 수 있습니다. hello 제한, hello 읽기에 대 한 자세한 toolearn [Azure 제한](../azure-subscription-service-limits.md#networking-limits) 문서.

### <a name="vnet-and-subnet-design"></a>VNet 및 서브넷 디자인
Nsg 적용된 toosubnets이 될 수 있으므로 서브넷으로 리소스를 그룹화 하 고 Nsg toosubnets 적용 하 여 hello 수가 Nsg 최소화할 수 있습니다.  Tooapply Nsg toosubnets 결정 한 경우에 기존 Vnet 및 있는 서브넷 되지 정의 된 Nsg에 주의 알 수 있습니다. NSG 디자인 toodefine 새 Vnet 및 서브넷 toosupport 필요 하 고 새 리소스 tooyour 새 서브넷을 배포할 수 있습니다. 다음 리소스 toohello 새 서브넷을 기존 마이그레이션 전략 toomove를 정의할 수 있습니다. 

### <a name="special-rules"></a>특별한 규칙
Hello 규칙에서 허용 하는 트래픽을 차단 하는 경우 인프라 핵심 Azure 서비스와 통신할 수 없습니다.

* **Hello 호스트 노드의 가상 IP:** DHCP, DNS 및 상태 모니터링을 통해 제공 됩니다 hello 가상화 된 호스트 IP 주소 168.63.129.16 같은 기본 인프라 서비스입니다. 이 공용 IP 주소 tooMicrosoft 속하고 hello만 가상화 된 IP 주소가이 용도로 모든 지역에서 사용 합니다. 이 IP 주소를 toohello 물리적 컴퓨터의 IP 주소를 hello 서버 (호스트 노드) hello VM 호스트를 매핑합니다. hello 호스트 노드는 부하 분산 장치 상태 프로브와 컴퓨터 상태 프로브의 hello hello DHCP 릴레이, DNS 재귀 확인자 hello, 및 hello에 대 한 hello 프로브 원본으로 작동 합니다. 통신 toothis IP 주소가 한 공격 않습니다.
* **라이선싱(키 관리 서비스)**: VM에서 실행되는 Windows 이미지를 사용하려면 라이선스가 있어야 합니다. tooensure 라이선스 요청을 이러한 쿼리를 처리 하는 toohello 키 관리 서비스 호스트 서버에 전송 됩니다. hello 요청은 포트 1688 통해 아웃 바운드 만들어집니다.

### <a name="icmp-traffic"></a>ICMP 트래픽
현재 NSG 규칙 hello 프로토콜만 허용 *TCP* 또는 *UDP*합니다. *ICMP*에 대한 고유 태그는 없습니다. 그러나 모든 포트와 프로토콜 hello VNet 내에서 트래픽을 tooand 있도록 hello AllowVNetInBound 기본 규칙에 의해 VNet 내에서 ICMP 트래픽이 허용 됩니다.

### <a name="subnets"></a>서브넷
* Hello 단계 수를의 사용자 작업에 필요한 것이 좋습니다. 서브넷에 NSG 적용 toohello 서브넷과 사용 하 여 각 계층을 격리 될 수 있습니다. 
* VPN 게이트웨이 또는 ExpressRoute 회로 대 한 tooimplement 서브넷을 필요한 경우에 **하지** NSG toothat 서브넷을 적용 합니다. 그렇게 하면 VNet 간 또는 온-프레미스 간 연결이 실패할 수 있습니다. 
* Tooimplement 해야 할 경우 네트워크 가상 어플라이언스 (NVA) hello NVA tooits 고유한 서브넷을 연결 하 고 hello NVA에서에서 사용자 정의 경로 (UDR) tooand를 만듭니다. 서브넷 수준 NSG toofilter 트래픽을이 서브넷 아웃을 구현할 수 있습니다. hello 읽을 UDRs에 대 한 자세한 toolearn [사용자 정의 경로](virtual-networks-udr-overview.md) 문서.

### <a name="load-balancers"></a>부하 분산 장치
* 각 작업에서 사용 하는 각 부하 분산 장치에 대 한 nat 규칙 hello 부하 분산 및 네트워크 주소를 고려 합니다. NAT 규칙은 Nic (리소스 관리자) 또는 Vm/클라우드 서비스 역할 인스턴스 (클래식)를 포함 하는 바인딩된 tooa 백 엔드 풀입니다. 만드는 각 백 엔드 풀에 대 한 NSG hello 부하 분산 장치에서 구현 된 hello 규칙을 통해 매핑된 트래픽만 허용 하는 것이 좋습니다. 각 백 엔드 풀에 대 한 NSG 만들기도 필터링 됩니다 (하지 않고 직접 hello 부하 분산 장치를 통해), toohello 백 엔드 풀 들어오는 트래픽을 보장 합니다.
* 클래식 배포 포트 역할 인스턴스 또는 Vm에서 부하 분산 장치 tooports에 매핑되는 끝점을 만듭니다. 또한 Resource Manager를 통해 사용자 고유의 개별적인 공용 부하 분산 장치를 만들 수도 있습니다. 들어오는 트래픽을 hello 대상 포트 hello hello VM에서에서 실제 포트 또는 역할 인스턴스를 부하 분산 장치에 의해 노출 된 hello 포트가 아닌 경우 hello 원본 포트 및 주소 hello 연결 toohello VM이 포트와 주소에 대 한 hello hello 포트 및 주소 hello 부하 분산 장치에 의해 노출 아닌 hello 인터넷에서에서 원격 컴퓨터.
* 내부 부하 분산 장치 ILB ()를 통해 들어오는 Nsg toofilter 트래픽을 만들면 hello 원본 컴퓨터를 하지 hello 부하 분산 장치에서에서 hello 원본 포트와 주소 범위 적용 됩니다. hello 대상 포트와 주소 범위는 hello 부하 분산 하지 hello 대상 컴퓨터의입니다.

### <a name="other"></a>기타
* 끝점 기반 액세스 제어 목록 (ACL) 및 Nsg hello에 지원 되지 않습니다 동일한 VM 인스턴스. Toouse NSG를 원하는 위치에 끝점 ACL을 이미 있는 경우 먼저 hello 끝점 ACL을 제거 합니다. 방법에 대 한 정보에 대 한 끝점 ACL tooremove 참조 hello [끝점 Acl을 관리](virtual-networks-acl-powershell.md) 문서.
* 리소스 관리자의 여러 Nic tooenable 관리 (원격 액세스) 당 NIC 별로 연결 된 NSG tooa NIC Vm에 대 한 사용할 수 있습니다. 고유한 Nsg tooeach NIC 연결 Nic에서 한 트래픽 유형 구분을 사용 합니다.
* 부하 분산 장치, 다른 Vnet의 트래픽을 필터링 하는 경우 비슷한 toohello 사용, 하지 hello Vnet를 연결 하는 hello 게이트웨이 hello 원격 컴퓨터의 hello 소스 주소 범위를 사용 해야 합니다.
* 여러 Azure 서비스에 연결 된 tooVNets 일 수 없습니다. Azure 리소스를 없는 경우 연결 된 tooa VNet에서 NSG toofilter 트래픽 toohello 리소스를 사용할 수 없습니다.  Hello 서비스에 대 한 hello 설명서를 읽기 사용 하면 toodetermine hello 서비스에 연결 된 VNet tooa 될 수 있습니다.

## <a name="sample-deployment"></a>샘플 배포
이 문서에서는 hello 정보의 tooillustrate hello 적용 hello 다음 그림에에서 표시 된 2 계층 응용 프로그램의 일반적인 시나리오를 고려 합니다.

![NSG](./media/virtual-network-nsg-overview/figure1.png)

Hello 다이어그램에 나와 있는 것 처럼 hello *Web1* 및 *Web2* Vm이 연결 된 toohello *프런트 엔드* 서브넷 및 hello *DB1* 및 *DB2* Vm이 연결 된 toohello *백 엔드* 서브넷입니다.  두 서브넷 hello의 일부인 *TestVNet* VNet입니다. hello 응용 프로그램 구성 요소 각 연결 된 Azure VM tooa VNet 내에서 실행합니다. hello 시나리오 요구 사항을 준수 하는 hello에 있습니다.

1. Hello 웹 및 DB 서버 간의 트래픽 분리 합니다.
2. 로드 균형 조정 규칙 hello 부하 분산 장치 tooall 웹 서버에서 포트 80에서 트래픽을 전달 합니다.
3. 분산 장치 NAT 규칙 트래픽을 전달 hello WEB1 VM에서 포트 50001 tooport 3389에 내용이 hello 부하 분산 장치에 로드 합니다.
4. 없음 액세스 toohello 2와 3의 요구 사항 제외 하 고 hello 인터넷에서에서 프런트 엔드 또는 백 엔드 Vm입니다.
5. 아웃 바운드 인터넷 액세스가 없는 hello 웹 또는 DB 서버에서 합니다.
6. Hello 프런트 엔드 서브넷에 대 한 액세스는 웹 서버의 3389 tooport를 허용 됩니다.
7. Hello 프런트 엔드 서브넷에 대 한 액세스는 DB 서버의 3389 tooport를 허용 됩니다.
8. Hello 프런트 엔드 서브넷에 대 한 액세스는 모든 DB 서버의 1433 tooport를 허용 됩니다.
9. DB 서버의 다른 NIC에서 관리 트래픽(3389 포트)과 데이터베이스 트래픽(1433 포트)을 분리합니다.

요구 사항 1-6 (제외 요구 사항 3 및 4)는 모든 예외일된 toosubnet 공간입니다. hello 다음 Nsg hello 이전 요구 사항을 충족 필요한 Nsg의 hello 수를 최소화 하는 동안:

### <a name="frontend"></a>FrontEnd
**인바운드 규칙**

| 규칙 | Access | 우선 순위 | 원본 주소 범위 | 원본 포트 | 대상 주소 범위 | 대상 포트 | 프로토콜 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-HTTP-Internet(인바운드 HTTP 인터넷 허용) | 허용 | 100 | 인터넷 | * | * | 80 | TCP |
| Allow-Inbound-RDP-Internet(인바운드 RDP 인터넷 허용) | 허용 | 200 | 인터넷 | * | * | 3389 | TCP |
| Deny-Inbound-All(모든 인바운드 거부) | 거부 | 300 | 인터넷 | * | * | * | TCP |

**아웃바운드 규칙**

| 규칙 | Access | 우선 순위 | 원본 주소 범위 | 원본 포트 | 대상 주소 범위 | 대상 포트 | 프로토콜 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All(모든 인터넷 거부) |거부 |100 | * | * | 인터넷 | * | * |

### <a name="backend"></a>BackEnd
**인바운드 규칙**

| 규칙 | Access | 우선 순위 | 원본 주소 범위 | 원본 포트 | 대상 주소 범위 | 대상 포트 | 프로토콜 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All(모든 인터넷 거부) | 거부 | 100 | 인터넷 | * | * | * | * |

**아웃바운드 규칙**

| 규칙 | Access | 우선 순위 | 원본 주소 범위 | 원본 포트 | 대상 주소 범위 | 대상 포트 | 프로토콜 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All(모든 인터넷 거부) | 거부 | 100 | * | * | 인터넷 | * | * |

다음 Nsg 만들어지고 tooNICs hello 다음 Vm에에서 연결 된 hello:

### <a name="web1"></a>WEB1
**인바운드 규칙**

| 규칙 | Access | 우선 순위 | 원본 주소 범위 | 원본 포트 | 대상 주소 범위 | 대상 포트 | 프로토콜 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-RDP-Internet(인바운드 RDP 인터넷 허용) | 허용 | 100 | 인터넷 | * | * | 3389 | TCP |
| Allow-Inbound-HTTP-Internet(인바운드 HTTP 인터넷 허용) | 허용 | 200 | 인터넷 | * | * | 80 | TCP |

> [!NOTE]
> hello 이전 규칙에 대 한 hello 소스 주소 범위는 **인터넷**, hello 부하 분산의 가상 IP 주소를 hello 되지 않습니다. hello 원본 포트는 *, 500001 하지 않습니다. 부하 분산 장치에 대 한 NAT 규칙 NSG 보안 규칙으로 동일한는 hello 있습니다. NSG 보안 규칙은 항상 관련된 toohello 원본 소스와의 트래픽 최종 대상 **하지** hello 2 사이 hello 부하 분산 장치입니다. 
> 
> 

### <a name="web2"></a>WEB2
**인바운드 규칙**

| 규칙 | Access | 우선 순위 | 원본 주소 범위 | 원본 포트 | 대상 주소 범위 | 대상 포트 | 프로토콜 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Inbound-RDP-Internet( 인바운드 RDP 인터넷 거부) | 거부 | 100 | 인터넷 | * | * | 3389 | TCP |
| Allow-Inbound-HTTP-Internet(인바운드 HTTP 인터넷 허용) | 허용 | 200 | 인터넷 | * | * | 80 | TCP |

### <a name="db-servers-management-nic"></a>DB 서버(관리 NIC)
**인바운드 규칙**

| 규칙 | Access | 우선 순위 | 원본 주소 범위 | 원본 포트 | 대상 주소 범위 | 대상 포트 | 프로토콜 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-RDP-Front-end(인바운드 RDP 프런트 엔드 허용) | 허용 | 100 | 192.168.1.0/24 | * | * | 3389 | TCP |

### <a name="db-servers-database-traffic-nic"></a>DB 서버(데이터베이스 트래픽 NIC)
**인바운드 규칙**

| 규칙 | Access | 우선 순위 | 원본 주소 범위 | 원본 포트 | 대상 주소 범위 | 대상 포트 | 프로토콜 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-SQL-Front-end(인바운드 SQL 프런트 엔드 허용) | 허용 | 100 | 192.168.1.0/24 | * | * | 1433 | TCP |

일부 hello Nsg 연결된 tooindividual Nic와 되므로 리소스 관리자를 통해 배포 된 리소스에 대 한 hello 규칙은입니다. 규칙은 연결되는 방법에 따라 서브넷과 NIC에 대해 결합됩니다. 

## <a name="next-steps"></a>다음 단계
* [NSG 배포(Resource Manager)](virtual-networks-create-nsg-arm-pportal.md).
* [NSG 배포(클래식)](virtual-networks-create-nsg-classic-ps.md).
* [NSG 로그를 관리](virtual-network-nsg-manage-log.md)합니다.
* [NSG 문제 해결](virtual-network-nsg-troubleshoot-portal.md)
