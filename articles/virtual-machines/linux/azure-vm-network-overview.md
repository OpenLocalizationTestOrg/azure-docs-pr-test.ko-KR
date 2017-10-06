---
title: "aaaAzure 및 Linux VM 네트워크 개요 | Microsoft Docs"
description: "Azure 및 Linux VM 네트워킹 개요입니다."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: b5420e35-0463-4456-9803-6142db150f2e
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: c3de2dc583c62160e10c0e97e96fef49b9eaffbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux-vm-network-overview"></a>Azure 및 Linux VM 네트워크 개요
## <a name="virtual-networks"></a>가상 네트워크
Azure 가상 네트워크 (VNet)는 hello 클라우드에서 사용자의 네트워크의 표현입니다. Azure 클라우드 전용 tooyour 구독 hello의 논리적 격리는 Hello IP 주소 블록, DNS 설정, 보안 정책 및이 네트워크 내에서 경로 테이블을 완벽 하 게 제어할 수 있습니다. 또한 VNet을 여러 서브넷으로 분할하고 Azure IaaS VM(가상 컴퓨터) 및/또는 Cloud Services(PaaS 역할 인스턴스)를 실행할 수 있습니다. 또한 Azure에서 사용할 수 있는 hello 연결 옵션 중 하나를 사용 하 여 hello 가상 네트워크 tooyour 온-프레미스 네트워크를 연결할 수 있습니다. 기본적으로 Azure에서 제공 하는 엔터프라이즈 규모의 hello 혜택을 사용 하 여 IP 주소 블록에 완벽 한 제어 하 여 네트워크 tooAzure 확장할 수 있습니다.

* [Virtual Network 개요](../../virtual-network/virtual-networks-overview.md)

사용 하 여 VNet toocreate hello Azure CLI, 이동 여기 toofollow hello 살펴봅니다.

* [사용 하 여 VNet toocreate Azure CLI hello 하는 방법](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

## <a name="network-security-groups"></a>네트워크 보안 그룹
네트워크 보안 그룹 NSG ()를 허용 하거나 거부 네트워크 트래픽을 가상 네트워크에서 VM 인스턴스 tooyour 액세스 제어 목록 (ACL) 규칙 목록이 포함 되어 있습니다. NSG는 서브넷 또는 서브넷 내의 개별 VM 인스턴스 중 하나와 연결될 수 있습니다. NSG를 서브넷과 연결 하는 경우 해당 서브넷에 tooall hello VM 인스턴스 hello ACL 규칙에 적용 됩니다. 또한 트래픽 tooan 개별 VM을 제한할 수 NSG를 연결 하 여 추가 VM toothat 직접 합니다.

* [NSG(네트워크 보안 그룹)란?](../../virtual-network/virtual-networks-nsg.md)
* [Toocreate Nsg에 Azure CLI hello 하는 방법](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

## <a name="user-defined-routes"></a>사용자 정의 경로
Azure에서 가상 컴퓨터 (Vm) tooa 가상 네트워크 (VNet)를 추가할 때 hello Vm은 서로 수 toocommunicate hello 네트워크를 통해 자동으로 확인할 수 있습니다. Hello Vm 서브넷이 서로 다른 경우에 게이트웨이 toospecify를 않아도 됩니다. hello 같은 기준이 hello Vm toohello에서 통신에 대 한 공용 인터넷 및 tooyour Azure에서 하이브리드 연결 데이터 센터를 사용할 수 있는지를 소유 하는 경우에 tooyour 온-프레미스 네트워크입니다.

* [사용자 정의 경로 및 IP 전달이란?](../../virtual-network/virtual-networks-udr-overview.md)
* [Hello Azure CLI에에서는 UDR 만들기](../../virtual-network/virtual-network-create-udr-arm-cli.md)

## <a name="associating-a-fqdn-tooyour-linux-vm"></a>FQDN tooyour Linux VM 연결
Hello Azure 포털에서에서 가상 컴퓨터 (VM)를 만들 때 hello 리소스 관리자 배포 모델을 공용 IP를 사용 하 여 리소스가 hello 가상 컴퓨터에 대 한 자동으로 생성 됩니다. VM이 IP 주소 tooremotely 액세스 hello를 사용 합니다. Hello 포털에서는 생성 하지는 정규화 된 도메인 이름 또는 FQDN으로 기본적으로 있지만 hello VM가 만들어지면 하나 추가할 수 있습니다.

* [Hello Azure 포털에서에서 정규화 된 도메인 이름 만들기](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="network-interfaces"></a>네트워크 인터페이스
네트워크 인터페이스 (NIC) hello 연결로 가상 컴퓨터 (VM) 및 기본 소프트웨어 네트워크 hello 사이입니다. 이 문서에서는 설명 네트워크 인터페이스 이며 hello Azure 리소스 관리자 배포 모델에서 사용 방법입니다.

* [가상 네트워크 인터페이스](../../virtual-network/virtual-network-network-interface.md)

## <a name="virtual-nics-and-dns-labeling"></a>가상 NIC 및 DNS 레이블 지정
Toobe 영구적으로 해야 하지만 해당 서버 캐 틀으로 처리 되 고 삭제 됩니다 서버 있고 자주 배포 toouse hello VNET에 있는 NIC toopersist hello 이름에 DNS 레이블을 지정 해야 합니다.  연습을 수행 하는 hello로 고정 ip 영구적으로 명명 된 NIC는 설치 합니다.

* [Hello Azure CLI를 사용 하 여 전체 Linux 환경 만들기](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="virtual-network-gateways"></a>가상 네트워크 게이트웨이
가상 네트워크 게이트웨이에 사용 되는 Azure 가상 네트워크와 온-프레미스 위치 간 및 Azure (VNet 대 VNet) 내에서 가상 네트워크 간의 toosend 네트워크 트래픽을 합니다. VPN Gateway를 구성할 때 가상 네트워크 게이트웨이 및 가상 네트워크 게이트웨이 연결을 만들고 구성해야 합니다.

* [VPN Gateway 정보](../../vpn-gateway/vpn-gateway-about-vpngateways.md)

## <a name="internal-load-balancing"></a>내부 부하 분산
Azure 부하 분산 장치는 계층 4(TCP, UDP) 부하 분산 장치입니다. hello 부하 분산 장치 부하 분산 장치 집합의 가상 컴퓨터 또는 클라우드 서비스의 비정상 상태 서비스 인스턴스 간에 들어오는 트래픽을 분산 하 여 고가용성을 제공 합니다. Azure Load Balancer는 여러 포트, 여러 IP 주소 또는 둘 다에서 이러한 서비스를 제공할 수도 있습니다.

* [Hello Azure CLI를 사용 하는 내부 부하 분산 장치 만들기](../../load-balancer/load-balancer-get-started-internet-arm-cli.md)

