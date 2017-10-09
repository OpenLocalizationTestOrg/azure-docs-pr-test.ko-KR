---
title: "Azure의 아웃 바운드 연결 aaaUnderstanding | Microsoft Docs"
description: "이 문서에서는 Azure Vm toocommunicate 공용 인터넷 서비스를 사용 하는 방법을 설명 합니다."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
ms.assetid: 5f666f2a-3a63-405a-abcd-b2e34d40e001
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 5/31/2017
ms.author: kumud
ms.openlocfilehash: ffe59971b934a16c9f6f78e3b15869a0072320d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-outbound-connections-in-azure"></a>Azure에서 아웃바운드 연결 이해

Azure의 VM(가상 컴퓨터)은 공용 IP 주소 공간에 있는 Azure 외부의 끝점과 통신할 수 있습니다. 공용 IP 주소 공간에는 아웃 바운드 흐름 tooa 대상을 시작 하는 VM을 Azure hello VM의 개인 IP 주소 tooa 공용 IP 주소 매핑하고 반환 트래픽을 tooreach hello VM을 허용 합니다.

Azure는 세 가지 방법을 tooachieve 아웃 바운드 연결을 제공합니다. 각 방법에는 고유한 기능 및 제약 조건이 있습니다. 각 메서드를 주의 깊게 검토 toochoose 어떤 필터가 요구 사항을 충족 합니다.

| 시나리오 | 메서드 | 참고 |
| --- | --- | --- |
| 독립 실행형 VM(부하 분산 장치 없음, 인스턴스 수준 공용 IP 주소 없음) |기본 SNAT |Azure에서는 SNAT에 공용 IP 주소를 연결합니다. |
| 부하 분산 VM(VM에 인스턴스 수준 공용 IP 주소 없음) |SNAT hello 부하 분산 장치를 사용 하 여 |Azure의 hello 부하 분산 장치는 공용 IP 주소를 사용 하 여 SNAT에 대 한 |
| 인스턴스 수준 공용 IP 주소를 가진 VM(부하 분산 장치 있음 또는 없음) |SNAT를 사용하지 않습니다. |Azure에서는 VM toohello 할당 hello 공용 IP |

공용 IP 주소 공간에는 Azure 외부에서 끝점이 있는 VM toocommunicate 하지 않으려면 보안 그룹 NSG (네트워크) tooblock 액세스를 사용할 수 있습니다. NSG를 사용하는 작업은 [공용 연결 방지](#preventing-public-connectivity)에서 더 자세하게 설명합니다.

## <a name="standalone-vm-with-no-instance-level-public-ip-address"></a>인스턴스 수준 공용 IP 주소 없는 독립 실행형 VM

이 시나리오에서는 hello VM Azure 부하 분산 장치 풀에 속하지 않는 및는 인스턴스 수준 공용 IP (ILPIP) 주소가 tooit 할당 되지 않습니다. Hello VM 아웃 바운드 흐름을 만들 때 Azure의 hello 아웃 바운드 흐름 tooa 공용 원본 IP 주소 hello 개인 원본 IP 주소를 변환 합니다. 이 아웃 바운드 흐름에 사용 되는 hello 공용 IP 주소를 구성할 수 없습니다 및 hello 구독 공용 IP 리소스 한계에 따라 계산 되지 않습니다. Azure 원본 네트워크 주소 변환 (SNAT) tooperform이이 함수를 사용합니다. Hello 공용 IP 주소의 사용 후 삭제 포트 사용 되는 toodistinguish 개별 흐름 hello VM에 의해 시작 됩니다. SNAT은 흐름이 만들어질 때 임시 포트를 동적으로 할당합니다. 이 컨텍스트에서 SNAT에 사용 되는 hello 사용 후 삭제 포트는 참조 된 tooas SNAT 포트입니다.

SNAT 포트는 소진될 수 있는 한정된 리소스입니다. 것이 중요 한 toounderstand 사용 되는 방법을 합니다. 흐름 tooa 단일 대상 IP 주소 당 하나의 SNAT 포트 소모 됩니다. 여러 흐름 toohello에 대 한 동일한 대상 IP 주소를 각 흐름 단일 SNAT 포트를 사용 합니다. 그러면 hello 흐름 고유한 경우에 발생 한 hello에서 동일한 공용 IP 주소 toohello 동일한 대상 IP 주소입니다. 여러 흐름 각 tooa 다른 대상 IP 주소는 대상 당 단일 SNAT 포트를 사용 합니다. hello 대상 IP 주소를 사용 하면 hello 흐름 고유 합니다.

사용할 수 있습니다 [부하 분산 장치에 대 한 로그 분석](load-balancer-monitor-log.md) 및 [SNAT 포트 소모 메시지에 대 한 경고 이벤트 로그 toomonitor](load-balancer-monitor-log.md#alert-event-log)합니다. SNAT 포트 리소스를 모두 사용한 경우 SNAT 포트가 기존 흐름에 의해 릴리스될 때까지 아웃바운드 흐름은 실패합니다. 부하 분산 장치는 SNAT 포트를 회수하는 데 4분의 유휴 시간 제한을 사용합니다.

## <a name="load-balanced-vm-with-no-instance-level-public-ip-address"></a>인스턴스 수준 공용 IP 주소가 없는 부하 분산 VM

이 시나리오에서는 hello VM에는 Azure 부하 분산 장치 풀의 일부입니다.  hello VM tooit 할당 된 공용 IP 주소를 없는 합니다. 부하 분산 장치 리소스 hello hello 백 엔드 풀과 규칙 toolink hello 공용 IP 프런트엔드로 구성 되어야 합니다.  이 구성을 완료 하지 않은 경우 hello 동작은 hello 위의 섹션에 설명 된 대로 [없는 인스턴스 수준 공용 IP를 사용 하 여 독립 실행형 VM](load-balancer-outbound-connections.md#standalone-vm-with-no-instance-level-public-ip-address)합니다.

Hello 부하 분산 된 VM을 만들 때 아웃 바운드 흐름 Azure의 hello 공용 부하 분산 장치 프런트 엔드의 hello 아웃 바운드 흐름 toohello 공용 IP 주소 hello 개인 원본 IP 주소를 변환 합니다. Azure 원본 네트워크 주소 변환 (SNAT) tooperform이이 함수를 사용합니다. Hello 부하 분산 장치의 공용 IP 주소의 사용 후 삭제 포트 사용 되는 toodistinguish 개별 흐름 hello VM에 의해 시작 됩니다. SNAT은 아웃바운드 흐름이 만들어질 때 임시 포트를 동적으로 할당합니다. 이 컨텍스트에서 SNAT에 사용 되는 hello 사용 후 삭제 포트는 참조 된 tooas SNAT 포트입니다.

SNAT 포트는 소진될 수 있는 한정된 리소스입니다. 것이 중요 한 toounderstand 사용 되는 방법을 합니다. 흐름 tooa 단일 대상 IP 주소 당 하나의 SNAT 포트 소모 됩니다. 여러 흐름 toohello에 대 한 동일한 대상 IP 주소를 각 흐름 단일 SNAT 포트를 사용 합니다. 그러면 hello 흐름 고유한 경우에 발생 한 hello에서 동일한 공용 IP 주소 toohello 동일한 대상 IP 주소입니다. 여러 흐름 각 tooa 다른 대상 IP 주소는 대상 당 단일 SNAT 포트를 사용 합니다. hello 대상 IP 주소를 사용 하면 hello 흐름 고유 합니다.

사용할 수 있습니다 [부하 분산 장치에 대 한 로그 분석](load-balancer-monitor-log.md) 및 [SNAT 포트 소모 메시지에 대 한 경고 이벤트 로그 toomonitor](load-balancer-monitor-log.md#alert-event-log)합니다. SNAT 포트 리소스를 모두 사용한 경우 SNAT 포트가 기존 흐름에 의해 릴리스될 때까지 아웃바운드 흐름은 실패합니다. 부하 분산 장치는 SNAT 포트를 회수하는 데 4분의 유휴 시간 제한을 사용합니다.

## <a name="vm-with-an-instance-level-public-ip-address-with-or-without-load-balancer"></a>인스턴스 수준 공용 IP 주소를 가진 VM(부하 분산 장치 있음 또는 없음)

이 시나리오에서는 hello VM에는 인스턴스 수준 공용 IP (ILPIP) tooit 할당 합니다. Hello VM에 부하 분산 또는 not 인지는 중요 하지 않습니다. ILPIP를 사용하는 경우 SNAT(원본 네트워크 주소 변환)을 사용하지 않습니다. hello VM에 대 한 모든 아웃 바운드 흐름 ILPIP hello를 사용합니다. 아웃 바운드 흐름을 시작 하는 응용 프로그램 SNAT 소모를 발생 하는 경우 ILPIP tooavoid SNAT 제약 조건을 지정 하는 것이 좋습니다.

## <a name="discovering-hello-public-ip-used-by-a-given-vm"></a>지정 된 VM에서 사용 하는 hello 공용 IP를 검색 합니다.

여러 가지 방법으로 아웃 바운드 연결의 toodetermine hello 공개 소스 IP 주소입니다. 확인할 수 있는 서비스를 제공 하는 OpenDNS hello VM의 공용 IP 주소입니다. Hello nslookup 명령 사용, hello 이름 myip.opendns.com toohello OpenDNS 확인자에 대 한 DNS 쿼리를 보낼 수 있습니다. hello 서비스를 사용 하는 toosend hello 쿼리 hello 원본 IP 주소를 반환 합니다. Hello VM에서 다음 쿼리를 실행 하면 hello 응답 hello 해당 VM에 대 한 공용 IP가 사용 됩니다.

    nslookup myip.opendns.com resolver1.opendns.com

## <a name="preventing-public-connectivity"></a>공용 연결 방지

경우에 따라 것은 바람직하지 않습니다 VM toobe toocreate 아웃 바운드 흐름을 허용 하거나 어떤 대상 아웃 바운드 전송에 접근할 수 요구 사항 toomanage 있을 수 있습니다. 이 경우에 사용 [보안 그룹 NSG (네트워크)](../virtual-network/virtual-networks-nsg.md) toomanage hello 대상 해당 hello VM에 도달할 수 있습니다. NSG를 적용 하는 경우 tooa 부하 분산 된 VM, toopay 주의 toohello 필요한 [태그 기본](../virtual-network/virtual-networks-nsg.md#default-tags) 및 [규칙 기본](../virtual-network/virtual-networks-nsg.md#default-rules)합니다.

해당 hello VM Azure 부하 분산 장치에서 상태 프로브 요청을 받을 수 있어야 합니다. NSG 블록 상태 프로브 요청 hello AZURE_LOADBALANCER 기본 태그에서에서 VM 상태 검색 실패 하 고 hello VM 가격 인하 됩니다. 부하 분산 장치 새 흐름 toothat VM을 보내는 것을 중지 합니다.

## <a name="limitations"></a>제한 사항

[여러(공용) IP 주소가 부하 분산 장치에 연결](load-balancer-multivip-overview.md)되는 경우 이러한 모든 공용 IP 주소는 아웃바운드 흐름의 후보입니다.

Azure는 알고리즘 toodetermine hello의 사용 가능한 SNAT 포트 hello 풀의 hello 크기에 따라 됩니다.  이 기능은 현재 구성 가능하지 않습니다.

사용할 수 있는 SNAT 포트 번호를 hello toorememember 의미 하지는 않습니다 직접 연결 toonumber 유용 합니다. 위 항목 보기 비슷하므로 때 및 SNAT 포트 할당 되는 방식과 toomanage이 exhaustible 리소스입니다.
