---
title: "aaaAzure 부하 분산 장치 개요 | Microsoft Docs"
description: "Azure 부하 분산 장치 기능, 아키텍처 및 구현에 대한 개요입니다. Hello 부하 분산 장치가 작동 하는 방법을 알아보고 hello 클라우드에서 활용 합니다."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
ms.assetid: 0f313dc0-f007-4cee-b2b9-f542357925a3
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 2376a02f7cbbbed6a90f216419c0c3d30f594272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-load-balancer-overview"></a>Azure 부하 분산 장치 개요

Azure 부하 분산 장치는 높은 가용성 및 네트워크 성능을 tooyour 응용 프로그램을 제공합니다. 이 장치는 부하 분산 장치 집합에 정의된 서비스의 정상 인스턴스 간에 들어오는 트래픽을 분산하는 계층 4(TCP, UDP) 부하 분산 장치입니다.

Azure Load Balancer를 다음과 같이 구성할 수 있습니다.

* 부하 분산 들어오는 인터넷 트래픽을 toovirtual 컴퓨터. 이 구성을 [인터넷 연결 부하 분산](load-balancer-internet-overview.md)이라고 합니다.
* 가상 네트워크의 가상 컴퓨터 간, 클라우드 서비스의 가상 컴퓨터 간 또는 크로스-프레미스 가상 네트워크의 온-프레미스 컴퓨터와 가상 컴퓨터 간에 트래픽을 부하 분산합니다. 이 구성을 [내부 부하 분산](load-balancer-internal-overview.md)이라고 합.
* 외부 트래픽이 tooa 특정 가상 컴퓨터를 전달 합니다.

Hello 클라우드의 모든 리소스 hello 인터넷에서에서 연결할 수 있는 공용 IP 주소 toobe가 필요합니다. Azure의 hello 클라우드 인프라는 해당 리소스에 대 한 라우팅할 수 없는 IP 주소를 사용합니다. Azure 공용 IP 주소 toocommunicate toohello 인터넷 인 네트워크 주소 변환 (NAT)를 사용합니다.

## <a name="azure-deployment-models"></a>Azure 배포 모델

Azure 클래식 hello 및 리소스 관리자 간의 중요 한 toounderstand hello 차이 [배포 모델](../azure-resource-manager/resource-manager-deployment-model.md)합니다. Azure Load Balancer는 각 모델에서 서로 다르게 구성됩니다.

### <a name="azure-classic-deployment-model"></a>Azure 클래식 배포 모델

클라우드 서비스 경계 내에서 배포 된 가상 컴퓨터 그룹화 부하 분산 장치 toouse 될 수 있습니다. 이 모델에서 공용 IP 주소 및 정규화 된 도메인 이름, (FQDN) tooa 클라우드 서비스에 할당 됩니다. hello 부하 분산 장치에서 번역 포트 하 고 부하 hello 클라우드 서비스에 대 한 hello 공용 IP 주소를 사용 하 여 hello 네트워크 트래픽을 분산 합니다.

부하 분산되는 트래픽은 끝점에 의해 정의됩니다. 포트 번역 끝점 hello 공용 IP 주소의 hello 공개 할당 된 포트와 toohello 서비스 특정 가상 컴퓨터에 할당 된 hello 로컬 포트 간의 한 일 관계가 있습니다. Hello 공용 IP 주소와 hello 할당 된 로컬 포트 toohello 서비스 간의 일 대 다 관계 hello 클라우드 서비스의 hello 가상 컴퓨터에 있어야 하는 부하 분산 끝점.

![Azure 부하 분산 장치 hello 클래식 배포 모델에](./media/load-balancer-overview/asm-lb.png)

그림 1-hello 클래식 배포 모델에서 Azure 부하 분산 장치

이 배포 모델에 대 한 부하 분산 장치 사용 하 여 hello 있는 hello 공용 IP 주소에 대 한 hello 도메인 레이블이 \<클라우드 서비스 이름\>. cloudapp.net에 합니다. hello 다음 그래픽에서는 Azure 부하 분산 장치 hello이 모델

### <a name="azure-resource-manager-deployment-model"></a>Azure Resource Manager 배포 모델

Hello 리소스 관리자 배포 모델의 경우 필요 toocreate 없는 클라우드 서비스 부하 분산 장치 hello tooexplicitly 여러 가상 컴퓨터 간의 트래픽은 라우팅합니다. 만들어집니다.

공용 IP 주소는 도메인 레이블(DNS 이름)이 있는 개별 리소스입니다. hello 공용 IP 주소는 hello 부하 분산 장치 리소스에 연결 합니다. 부하 분산 장치 규칙 및 인바운드 NAT 규칙의 부하 분산 된 네트워크 트래픽을 수신 하는 hello 리소스에 대 한 인터넷 끝점 hello으로 hello 공용 IP 주소를 사용 합니다.

개인 또는 공용 IP 주소를 toohello 네트워크 인터페이스 연결 된 리소스 tooa 가상 컴퓨터에 할당 됩니다. 네트워크 인터페이스 tooa 부하 분산 장치의 백 엔드 IP 주소 풀에 추가 되 면 hello 부하 분산 장치는 수 toosend 부하 분산 된 네트워크 트래픽 규칙에 따라 hello 부하가 생성 됩니다.

hello 다음 그래픽에서는 hello Azure 부하 분산 장치가이 모델:

![Resource Manager에서 Azure Load Balancer](./media/load-balancer-overview/arm-lb.png)

그림 2 - Resource Manager의 Azure Load Balancer

리소스 관리자 기반 서식 파일, Api 및 도구를 통해 hello 부하 분산 장치를 관리할 수 있습니다. toolearn 더에 대 한 리소스 관리자 참조 hello [리소스 관리자 개요](../azure-resource-manager/resource-group-overview.md)합니다.

## <a name="load-balancer-features"></a>부하 분산 장치 기능

* 해시 기반 배포

    Azure 부하 분산 장치는 해시 기반 배포 알고리즘을 사용합니다. 기본적으로 5-튜플 해시는 원본 IP, 원본 포트, 대상 IP, 대상 포트 및 프로토콜 유형 toomap 트래픽 tooavailable 서버 구성 사용 합니다. 전송 세션 *내에서만* 연결이 유지됩니다. 동일한 TCP 또는 UDP 세션이 hello 패킷에 toohello hello 부하 분산 된 끝점 뒤 동일한 인스턴스를 이동 합니다. Hello 클라이언트 및 hello 연결을 다시 열 닫거나 hello에서 새 세션을 시작 하는 경우 원본 IP, 원본 포트 변경 내용을 hello 동일한. 이 hello 트래픽 toogo tooa 다른 끝점에서 다른 데이터 센터 않을 수 있습니다.

    자세한 내용은 [부하 분산 장치 배포 모드](load-balancer-distribution-mode.md)를 참조하세요. hello 다음 그래픽 표시 hello 해시 기반 배포:

    ![해시 기반 배포](./media/load-balancer-overview/load-balancer-distribution.png)

    그림 3 - 해시 기반 배포

* 포트 전달

    Azure 부하 분산 장치는 어떻게 인바운드 통신이 관리되는 방법을 제어할 수 있습니다. 이 통신은 인터넷 호스트, 다른 클라우드 서비스의 가상 컴퓨터 또는 가상 네트워크에서 시작된 트래픽을 포함합니다. 이 제어는 끝점(입력 끝점이라고도 함)으로 표시됩니다.

    입력된 끝점 공용 포트에서 수신 하 고 트래픽을 tooan 내부 포트를 전달 합니다. 내부 또는 외부 끝점에 대 한 포트 동일 hello 매핑하거나 다른 포트를 사용 하 여를 수 있습니다. 예를 들어 hello 공용 끝점 매핑은 포트 80 웹 구성 된 서버 toolisten tooport 81을 사용할 수 있습니다. 공용 끝점을 만들면을 hello hello 부하 분산 장치 인스턴스를 만드는 과정을 트리거합니다.

    Azure 포털을 hello 사용 하 여 만든, hello 포털 hello 프로토콜 RDP (원격 데스크톱)에 대 한 끝점 toohello 가상 컴퓨터 및 원격 Windows PowerShell 세션 트래픽용으로 자동으로 만듭니다. 이러한 끝점을 사용할 수 있습니다 tooremotely hello 인터넷을 통해 hello 가상 컴퓨터를 관리 합니다.

* 자동 재구성

    Azure 부하 분산 장치는 인스턴스를 확장 또는 축소하는 경우 즉시 재구성됩니다. 예를 들어 이러한 재구성 늘리면 hello 클라우드 서비스에서 웹/작업자 역할 인스턴스 수 또는 발생 hello에 추가 가상 컴퓨터를 추가 하면 부하가 동일한 설정 합니다.

* 서비스 모니터링

    Azure 부하 분산 장치 hello의 hello 상태 다양 한 서버 인스턴스를 검색할 수 있습니다. Toorespond는 검색이 실패 하면 새 연결 toohello 비정상 인스턴스를 보내는 hello 부하 분산 장치 중지 됩니다. 기존 연결은 영향을 받지 않습니다.

    지원되는 세 가지 형식의 프로브가 있습니다.

    + **게스트 에이전트 프로브 (on 플랫폼으로는 서비스 가상 컴퓨터에만):** hello 부하 분산 장치에서 hello 가상 컴퓨터 내의 게스트 에이전트 hello를 사용 합니다. hello 게스트 에이전트에서 수신 하 여 인스턴스는 hello 준비 상태에는 HTTP 200 정상 응답 경우에 hello를 사용 하 여 응답 (예: hello 인스턴스는 상태가 아니므로 없음, 처럼 재활용, 또는 중지) 합니다. Hello 에이전트가 HTTP 200 OK와 toorespond 실패 hello 부하 분산 장치 표시 hello 인스턴스를 응답 없음으로 / 중지 toothat 인스턴스에 트래픽을 전송 합니다. 부하 분산 장치 hello tooping hello 인스턴스를 계속합니다. Hello 게스트 에이전트가 HTTP 200에 응답 하는 경우 hello 부하 분산 장치는 트래픽을 toothat 인스턴스를 다시 전송 합니다. 웹 역할을 사용 하는 웹 사이트 코드는 일반적으로 hello Azure 패브릭 또는 게스트 에이전트에서 모니터링 하지 않는 w3wp.exe에서 실행 됩니다. 이 오류 (예: HTTP 500 응답) w3wp.exe에 보고 된 toohello 게스트 에이전트 수 없으며 hello 부하 분산 장치는 알지 못합니다 tootake 해당 인스턴스가 회전 하지 의미 합니다.
    + **사용자 지정 프로브를 HTTP:** 이 프로브는 hello 기본 (게스트 에이전트) 프로브를 재정의 합니다. Toocreate 사용 하려면 사용자 고유의 사용자 지정 논리 toodetermine hello hello 역할 인스턴스의 상태입니다. hello 부하 분산 장치 끝점 (기본적으로 모든 15 초)을 검색 정기적으로 합니다. hello 인스턴스 hello 제한 시간 (기본값은 31 초) 내 ACK TCP 또는 HTTP 200를 사용 하 여 응답 차례 대로 toobe를 간주 합니다. 이 hello 부하 분산 장치의 회전에서 직접 논리 tooremove 인스턴스를 구현 하는 데 유용 합니다. 예를 들어 hello 인스턴스 CPU 사용률이 90% 보다 크면 hello 인스턴스 tooreturn-200 상태를 구성할 수 있습니다. W3wp.exe를 사용 하는 웹 역할에 대 한도 얻게 자동 오류 코드를 웹 사이트에 200 이외의 상태 toohello 프로브를 반환 하므로 웹 사이트에 대 한 모니터링 합니다.
    + **사용자 지정 TCP 프로브:** 이 검색이 성공 TCP 세션 설정이 정의 tooa 프로브 포트에 의존 합니다.

    자세한 내용은 참조 hello [LoadBalancerProbe 스키마](https://msdn.microsoft.com/library/azure/jj151530.aspx)합니다.

* 원본 NAT

    서비스에서 시작 된 인터넷에서 모든 아웃 바운드 트래픽을 toohello NAT (SNAT)를 사용 하 여 원본으로 들어오는 트래픽을 hello 동일한 VIP 주소를 hello 합니다. SNAT에는 다음과 같은 중요한 이점이 있습니다.

    + VIP 수 동적으로 hello tooanother hello 서비스 인스턴스의 매핑되어 있으므로 쉽게 업그레이드 및 재해 복구를 서비스의 수 있습니다.
    + ACL(액세스 제어 목록)을 보다 쉽게 관리할 수 있습니다. VIP로 표현되는 ACL은 서비스를 강화하거나 규모를 축소하거나 다시 배포해도 변경되지 않습니다.

    hello 부하 분산 장치 구성 UDP에 대 한 전체 원뿔 NAT를 지원합니다. 전체 원뿔 NAT는 여기서 hello 포트 연결을 허용 인바운드 모든 외부 호스트 로부터 (응답 tooan 아웃 바운드 요청)의 NAT의 형식입니다.

    가상 컴퓨터를 시작 하는 각 새 아웃 바운드 연결에 대해 아웃 바운드 포트 hello 부하 분산 장치에 의해 할당 됩니다. 외부 호스트 hello 가상 VIP IP 할당 된 포트를 사용 하 여 트래픽을 볼 수 있습니다. 많은 수의 아웃 바운드 연결을 필요로 하는 시나리오에 대 한 것이 좋습니다 toouse [인스턴스 수준 공용 IP](../virtual-network/virtual-networks-instance-level-public-ip.md) 주소를 hello Vm SNAT에 대 한 아웃 바운드 전용된 IP 주소가 있어야 합니다. 이 포트 소모의 hello 위험을 줄입니다.

    이 항목에 대한 자세한 내용은 [아웃바운드 연결](load-balancer-outbound-connections.md) 문서를 참조하세요.

### <a name="support-for-multiple-load-balanced-ip-addresses-for-virtual-machines"></a>가상 컴퓨터에 대해 여러 개의 부하 분산 IP 주소 지원
둘 이상의 부하 분산 된 공용 IP 주소 tooa 집합의 가상 컴퓨터를 할당할 수 있습니다. 이러한 기능을 통해 여러 SSL 웹 사이트 및/또는 가상 컴퓨터의 설정 같은 hello에 여러 명의 SQL Server AlwaysOn 가용성 그룹 수신기를 호스트할 수 있습니다. 자세한 내용은 [클라우드 서비스당 여러 VIP](load-balancer-multivip.md)를 참조하세요.

[!INCLUDE [load-balancer-compare-tm-ag-lb-include.md](../../includes/load-balancer-compare-tm-ag-lb-include.md)]

## <a name="limitations"></a>제한 사항

부하 분산 장치 백 엔드 풀에는 기본 계층을 제외한 모든 VM SKU가 포함될 수 있습니다.

## <a name="next-steps"></a>다음 단계

- [인터넷 연결 Load Balancer](load-balancer-internet-overview.md)에 대해 알아보기

- [내부 Load Balancer 개요](load-balancer-internal-overview.md)에 대해 알아보기

- [인터넷 연결 Load Balancer](load-balancer-get-started-internet-portal.md) 만들기

- 일부 hello에 대 한 자세한 내용은 다른 키 [네트워킹 기능](../networking/networking-overview.md) azure

