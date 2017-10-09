---
title: "Azure 부하 분산 장치에 대 한 ipv6 aaaOverview | Microsoft Docs"
description: "Azure Load Balancer 및 부하 분산된 VM에 대한 IPv6 지원 이해하기."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
keywords: "ipv6, Azure Load Balancer, 이중 스택, 공용 IP, 기본 ipv6, 모바일, iot"
ms.assetid: 6a1d583f-a305-40fd-a94b-fa42e1943bbb
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: 5b203f77d86cc1ad455f4ebb297097aef46b658d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-ipv6-for-azure-load-balancer"></a>Azure Load Balancer의 IPv6에 대한 개요

인터넷 연결 부하 분산 장치는 IPv6 주소를 사용해 배포할 수 있습니다. 또한 tooIPv4 연결,이 통해 기능을 수행 하는 hello:

* 기본 종단 간 IPv6 연결 공용 인터넷 클라이언트와 Azure 가상 컴퓨터 (Vm) 사이의 hello 부하 분산 장치를 통해.
* VM과 공용 인터넷 IPv6 사용 가능 클라이언트 사이의 네이티브 종단 간 IPv6 아웃바운드 연결.

다음 그림 hello Azure 부하 분산 장치에 대 한 hello IPv6 기능을 설명 합니다.

![IPv6를 사용하여 Azure Load Balancer](./media/load-balancer-ipv6-overview/load-balancer-ipv6.png)

배포 된 후 IPv4 또는 IPv6 가능 인터넷 클라이언트 hello 공용 IPv4 또는 IPv6 주소 (또는 호스트 이름)의 Azure 인터넷 연결 부하 분산 장치 hello와 통신할 수 있습니다. hello 부하 분산 장치 경로 hello hello vm 네트워크 주소 변환 (NAT)를 사용 하 여 IPv6 패킷 toohello 개인 IPv6 주소입니다. hello IPv6 인터넷 클라이언트 hello hello Vm의 IPv6 주소와 직접 통신할 수 없습니다.

## <a name="features"></a>기능

Azure Resource Manager를 통해 배포된 VM에 대한 네이티브 IPv6 지원은 다음을 제공합니다.

1. IPv6 hello 인터넷에 있는 클라이언트에 대 한 IPv6 서비스 부하 분산
2. VM의 네이티브 IPv6 및 IPv4 끝점("이중 스택됨")
3. 인바운드 및 아웃바운드 시작 네이티브 IPv6 연결
4. TCP, UDP, HTTP(S)와 같은 지원되는 프로토콜은 서비스 아키텍처의 전체 범위를 사용하도록 설정합니다.

## <a name="benefits"></a>이점

이 기능을 통해 주요 이점은 다음 hello:

* 새 응용 프로그램에 액세스할 수 있는 tooIPv6 으로만 이동 가능한 클라이언트 수 없어도 정부 규정을 준수
* Enable 모바일 및 IOT (사물) 개발자 toouse 이중 누적 (IPv6 + IPv4) Azure 가상 컴퓨터 tooaddress의 인터넷 hello 증가 모바일 및 IOT 시장

## <a name="details-and-limitations"></a>세부 사항 및 제한 사항

세부 정보

* hello Azure DNS 서비스 IPv4 A 및 AAAA IPv6 모두 이름 레코드를 포함 하며 hello 부하 분산 장치에 대 한 두 레코드를 사용 하 여 응답 합니다. hello 클라이언트와 어떤 주소 (IPv4 또는 IPv6) toocommunicate를 선택합니다.
* VM 시작 연결 tooa 공용 IPv6 인터넷에 연결 된 장치, 네트워크 주소 변환 hello 부하 분산 장치 (NAT) toohello 공용 IPv6 주소 hello VM의 source IPv6 주소는 합니다.
* Hello Linux 운영 체제를 실행 하는 Vm에 구성 된 tooreceive DHCP 통해 IPv6 IP 주소 여야 합니다. Azure 갤러리는 이미 hello hello Linux 이미지의 많은 toosupport IPv6 수정 하지 않고 구성. 자세한 내용은 [Linux VM에 대한 DHCPv6 구성](load-balancer-ipv6-for-linux.md)
* 선택 하는 경우 사용자 부하 분산 장치 상태 프로브 toouse IPv4 프로브를 만들고 hello IPv4 및 IPv6 끝점 모두와 함께 사용 합니다. VM에 hello 서비스가 다운 되 면 hello IPv4 및 IPv6 끝점 모두 순환 순서에서 수행 됩니다.

제한 사항

* Hello Azure 포털에서에서 IPv6 부하 분산 규칙을 추가할 수 없습니다. hello 규칙 CLI, PowerShell hello 템플릿을 통해만 만들 수 있습니다.
* 기존 Vm toouse IPv6 주소를 업그레이드 하지 않을 수 있습니다. 새 VM을 배포해야 합니다.
* 각 VM에서 tooa 단일 네트워크 인터페이스가 단일 IPv6 주소를 할당할 수 있습니다.
* IPv6 주소를 공개 하는 hello tooa VM을 할당할 수 없습니다. 부하 분산 장치 tooa 할당만 하기.
* 공용 IPv6 주소에 대 한 hello 역방향 DNS 조회를 구성할 수 없습니다.
* hello IPv6 주소가 포함 된 hello Vm에는 Azure 클라우드 서비스의 구성원 일 수 없습니다. 연결 된 Azure 가상 네트워크 (VNet) tooan 하 고의 IPv4 주소를 통해 서로 통신할 수 있습니다.
* 개인 IPv6 주소를 리소스 그룹의 개별 VM에 배포할 수 있지만 확장 집합을 통해 리소스 그룹에 배포할 수는 없습니다.
* Azure Vm은 IPv6 tooother Vm, 다른 Azure 서비스 또는 온-프레미스 장치를 통해 연결할 수 없습니다. I p v 6을 통해만 hello Azure 부하 분산 장치와 통신할 수 있습니다. 그러나 IPv4를 사용하면 이러한 다른 리소스와 통신할 수 있습니다.
* IPv4에 대한 Network Security Group (NSG) 보호는 이중 스택 (IPv6+IPv4) 배포에서 지원됩니다. Nsg은 toohello IPv6 끝점 적용 되지 않습니다.
* IPv6 hello 끝점 VM이 아닌 hello에 직접 노출 toohello 인터넷 합니다. 부하 분산 장치 뒤에.있습니다. Hello 부하 분산 장치 규칙에 지정 된 hello 포트만 i p v 6을 통해 액세스할 수 있습니다.
* I p v 6은 IdleTimeout 매개 변수를 hello 변경 **현재 지원 되지 않는**합니다. hello 기본값은 4 분입니다.
* I p v 6은 loadDistributionMethod 매개 변수를 hello 변경 **현재 지원 되지 않는**합니다.
* 예약된 IPv6 IP(여기서 IPAllocationMethod = static)는 **현재 지원되지 않습니다**.

## <a name="next-steps"></a>다음 단계

자세한 내용은 방법 toodeploy i p v 6는 부하 분산 장치입니다.

* [지역별 IPv6 가용성](https://go.microsoft.com/fwlink/?linkid=828357)
* [템플릿을 사용하여 IPv6와 함께 부하 분산 장치 배포하기](load-balancer-ipv6-internet-template.md)
* [Azure PowerShell을 사용하여 IPv6와 함께 부하 분산 장치 배포하기](load-balancer-ipv6-internet-ps.md)
* [Azure CLI를 사용하여 IPv6와 함께 부하 분산 장치 배포하기](load-balancer-ipv6-internet-cli.md)
