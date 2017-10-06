---
title: "Azure 부하 분산 장치에 대 한 Vip aaaMultiple | Microsoft Docs"
description: "Azure Load Balancer의 다중 VIP에 대한 개요"
services: load-balancer
documentationcenter: na
author: chkuhtz
manager: narayan
editor: 
ms.assetid: 748e50cd-3087-4c2e-a9e1-ac0ecce4f869
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/11/2016
ms.author: chkuhtz
ms.openlocfilehash: e186e1248e7d187e7efd0668dc3244465ce3e156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-vips-for-azure-load-balancer"></a>Azure Load Balancer에 대한 다중 VIP

Azure 부하 분산 장치 tooload 균형 서비스를 여러 포트, 여러 개의 IP 주소 또는 둘 다 있습니다. Vm의 조합에 대해 public 및 내부 부하 분산 장치 정의 tooload 균형 흐름을 사용할 수 있습니다.

이 문서에서는이 기능, 중요 한 개념 및 제약 조건의 fundamentals hello를 설명 합니다. 하나의 IP 주소에 tooexpose 서비스만 가져오려는 경우에 대 한 간단한 지침을 찾을 수 있습니다 [공용](load-balancer-get-started-internet-portal.md) 또는 [내부](load-balancer-get-started-ilb-arm-portal.md) 부하 분산 장치 구성 합니다. 여러 Vip를 추가 하는 것은 증분 tooa 단일 VIP 구성입니다. 이 문서의 hello 개념을 사용 하 여, 언제 든 지 단순화 된 구성을 확장할 수 있습니다.

Azure Load Balancer를 정의할 때 프런트 엔드 및 백 엔드 구성이 규칙과 연결됩니다. hello hello 규칙에서 참조 하는 상태 검색은 사용 되는 toodetermine 새로운 흐름 hello 백 엔드 풀의 tooa 노드 전송 됩니다. hello 프런트 엔드는 여는 VIP (가상 IP), IP 주소 (공용 또는 내부), (UDP 또는 TCP) 전송 프로토콜 및 포트 번호를 구성 하는 3-튜플은 정의 되어 있습니다. DIP는 가상 NIC Azure의 IP 주소를 tooa hello 백 엔드 풀에서 VM을 연결 합니다.

다음 표에 hello 일부 예제에서는 프런트 엔드 구성은 포함 되어 있습니다.

| VIP | IP 주소 | protocol | 포트 |
| --- | --- | --- | --- |
| 1 |65.52.0.1 |TCP |80 |
| 2 |65.52.0.1 |TCP |*8080* |
| 3 |65.52.0.1 |*UDP* |80 |
| 4 |*65.52.0.2* |TCP |80 |

hello 표에서 4 개의 다른 프런트엔드 보여 줍니다. 프런트 엔드 #1, # 2 및 #3는 여러 규칙을 가진 단일 VIP입니다. hello 동일한 IP 주소를 사용 하지만 hello 포트 또는 프로토콜은 각 프런트 엔드 마다 다릅니다. 프런트엔드 # 1과 4은 여기서 hello 동일한 프런트 엔드 프로토콜 및 포트 다시 사용 된 여러 vip가에서 여러 vip가의 예입니다.

Azure 부하 분산 장치는 hello 부하 분산 규칙 정의에 유연성을 제공 합니다. 규칙 주소 및 포트 hello 프런트 엔드에 매핑된 toohello 대상 주소와 포트 hello 백 엔드에는 하는 방법을 선언 합니다. 규칙에서 백 엔드 포트 다시 사용 된 여부 hello 유형의 hello 규칙에 따라 달라 집니다. 각 규칙 유형에는 호스트 구성 및 프로브 디자인에 영향을 줄 수 있는 특정 요구 사항이 있습니다. 다음과 같은 두 가지 규칙 유형이 있습니다.

1. 백 엔드 포트가 없는와 hello 기본 규칙을 다시 사용
2. 백 엔드 포트는 다시 사용 하는 hello 부동 IP 규칙

Azure 부하 분산 장치는 모두 규칙 유형에 toomix 허용 hello 동일한 부하 분산 장치 구성 합니다. hello 부하 분산 장치에 사용할 수 동시에 지정 된 VM 또는 조합으로 hello 규칙의 hello 제약 조건에 의해 준수 합니다. 규칙 유형을 선택 하면 해당 구성을 지 원하는 응용 프로그램 및 hello 복잡성 프로그램의 hello 요구 사항에 따라 달라 집니다. 어떤 규칙 유형이 시나리오에 가장 적합한지 평가해야 합니다.

Hello 기본 동작을 사용 하 여 이러한 시나리오를 보다을 탐색 합니다.

## <a name="rule-type-1-no-backend-port-reuse"></a>규칙 유형 #1: 백 엔드 포트 재사용하지 않음.

![MultiVIP 그림](./media/load-balancer-multivip-overview/load-balancer-multivip.png)

이 시나리오에서는 hello 프런트 엔드 Vip는 다음과 같이 구성 됩니다.

| VIP | IP 주소 | protocol | 포트 |
| --- | --- | --- | --- |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |*65.52.0.2* |TCP |80 |

hello DIP는 hello의 hello 대상 흐름 인바운드 합니다. Hello 백 엔드 풀의 각 VM에서 DIP에 고유한 포트 hello 필요한 서비스를 노출합니다. 이 서비스는 규칙 정의 통해 hello 프런트 엔드 연관 되어 있습니다.

두 가지 규칙을 정의합니다.

| 규칙 | 맵 프론트 엔드 | toobackend 풀 |
| --- | --- | --- |
| 1 |![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 |![백 엔드](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) DIP1:80, ![백 엔드](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) DIP2:80 |
| 2 |![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 |![백 엔드](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) DIP1:81, ![백 엔드](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) DIP2:81 |

Azure 부하 분산 장치에서 전체 매핑 hello는 이제 다음과 같습니다.

| 규칙 | VIP IP 주소 | protocol | 포트 | 대상 | 포트 |
| --- | --- | --- | --- | --- | --- |
| ![규칙](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |DIP IP 주소 |80 |
| ![규칙](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |65.52.0.2 |TCP |80 |DIP IP 주소 |81 |

각 규칙은 대상 IP 주소 및 대상 포트의 고유한 조합으로 흐름을 생성해야 합니다. Hello 흐름의 다양 한 hello 대상 포트가 동일한 DIP 서로 다른 포트에서 여러 규칙 흐름 toohello 제공할 수 있습니다.

상태 검색이 directed toohello VM의 DIP는 항상입니다. 확인 해야 하면 프로그램 프로브 hello VM의 hello 상태를 반영 합니다.

## <a name="rule-type-2-backend-port-reuse-by-using-floating-ip"></a>규칙 유형 #2: 부동 IP를 사용하여 백엔드 포트 재사용

Azure 부하 분산 장치 hello 유연성 tooreuse hello 프런트 엔드 포트에서 사용 되는 hello 규칙 종류에 관계 없이 여러 vip가 제공 합니다. 또한 일부 응용 프로그램 시나리오 선호 또는 hello toobe hello 백 엔드 풀의 단일 VM의 여러 응용 프로그램 인스턴스에 사용 되는 동일한 포트 필요로 합니다. 포트 재사용의 일반적인 예에는 고가용성을 위한 클러스터링, 네트워크 가상 어플라이언스 및 재암호화 없이 다중 TLS 끝점 노출이 포함됩니다.

여러 규칙에서 tooreuse hello 백 엔드 포트를 원하는 경우에 hello 규칙 정의에 부동 IP를 활성화 해야 합니다.

부동 IP는 Direct Server Return (DSR)으로 알려진 것의 일부입니다. DSR는 흐름 토폴로지와 IP 주소 매핑 구성표라는 두 부분으로 구성됩니다. 플랫폼 수준에서 Azure Load Balancer는 부동 IP 사용 여부에 관계 없이 DSR 흐름 토폴로지에서 항상 작동합니다. 이 흐름의 아웃 바운드 일부 hello은 항상 올바르게 다시 쓴된 tooflow 직접 백 toohello 원점 것을 의미 합니다.

Azure는 hello 기본 규칙 종류와 기존 부하 분산 사용 편의성에 대 한 IP 주소 매핑 구성표를 노출 합니다. 부동 IP를 사용할 수 있도록 유연성이 아래 설명 참조에 대 한 IP 주소 매핑 구성표 tooallow hello를 변경합니다.

hello 다음 다이어그램에서는이 구성을 수행 합니다.

![MultiVIP 그림](./media/load-balancer-multivip-overview/load-balancer-multivip-dsr.png)

이 시나리오에서는 hello 백 엔드 풀의 모든 VM에 3 개의 네트워크 인터페이스가 있습니다.

* DIP: hello VM (Azure의 NIC 리소스의 IP 구성)와 관련 된 한 가상 NIC
* VIP1: VIP1의 IP 주소로 구성된 게스트 OS 내의루프백 인터페이스
* VIP2: VIP2의 IP 주소로 구성된 게스트 OS 내의루프백 인터페이스

> [!IMPORTANT]
> hello 논리 인터페이스의 hello 구성은 hello 게스트 운영 체제 내에서 수행 됩니다. 이 구성은 Azure에서 수행하거나 관리하지 않습니다. 이 구성이 없으면 hello 규칙이 작동 하지 않습니다. 상태 프로브 정의 논리 VIP hello 않고 hello hello VM의 DIP를 사용 합니다. 따라서 서비스는 hello 논리 VIP에서 제공 하는 hello 서비스의 hello 상태를 반영 하는 DIP 포트에서 프로브 응답을 제공 해야 합니다.

Hello를 가정해 보겠습니다 hello 이전 시나리오에서와 같이 동일한 프런트 엔드 구성:

| VIP | IP 주소 | protocol | 포트 |
| --- | --- | --- | --- |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |*65.52.0.2* |TCP |80 |

두 가지 규칙을 정의합니다.

| 규칙 | 맵 프론트 엔드 | toobackend 풀 |
| --- | --- | --- |
| 1 |![규칙](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 |![백 엔드](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 (VM1 및 VM2에서) |
| 2 |![규칙](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 |![백 엔드](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 (VM1 및 VM2에서) |

다음 표에서 hello hello 부하 분산 장치에서 hello 전체 매핑을 보여 줍니다.

| 규칙 | VIP IP 주소 | protocol | 포트 | 대상 | 포트 |
| --- | --- | --- | --- | --- | --- |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |VIP (65.52.0.1)과 동일함 |VIP (80)과 동일함 |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |65.52.0.2 |TCP |80 |VIP (65.52.0.2)과 동일함 |VIP (80)과 동일함 |

hello 대상의 hello 인바운드 흐름은 VM hello hello 루프백 인터페이스에서 hello VIP 주소입니다. 각 규칙은 대상 IP 주소 및 대상 포트의 고유한 조합으로 흐름을 생성해야 합니다. 다양 한 hello 대상 IP 주소로 hello 흐름의 포트를 재사용할 수 있기에 동일한 VM hello 합니다. 사용자 서비스 toohello VIP의 IP 주소와 포트 hello 해당 루프백 인터페이스를 바인딩하여 노출된 toohello 부하 분산 장치는입니다.

이 예제에서는 hello 대상 포트를 변경 하지 않습니다 확인 합니다. 이 값은 부동 IP 시나리오, Azure 부하 분산 장치도 지원 규칙 toorewrite hello 백 엔드 대상 포트 및 toomake 정의 다름 hello 프런트 엔드 대상 포트입니다.

hello 부동 IP 규칙 종류는 여러 가지 부하 분산 장치 구성 패턴의 hello 기반 합니다. 현재 사용할 수 있는 한 가지 예는 hello [여러 수신기와 함께 SQL AlwaysOn](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md) 구성 합니다. 앞으로 이러한 시나리오 더욱 자세히 설명할 것입니다.

## <a name="limitations"></a>제한 사항

* 다중 VIP 구성은 IaaS VM을 사용할 때만 지원됩니다.
* Hello 부동 IP 규칙을 사용 하면 응용 프로그램 아웃 바운드 전송에 대 한 hello DIP를 사용 해야 합니다. 응용 프로그램 hello 게스트 OS의에서 hello 루프백 인터페이스에 구성 된 toohello VIP 주소를 바인딩할 경우 다음 SNAT 사용할 수 있는 toorewrite hello에 대 한 아웃 바운드 흐름 아니며 hello 흐름 실패.
* 공용 IP 주소는 대금 청구에 영향을 미칩니다. 자세한 내용은 [IP 주소 가격 책정](https://azure.microsoft.com/pricing/details/ip-addresses/)
* 구독 제한이 적용됩니다. 자세한 내용은 [서비스 제한](../azure-subscription-service-limits.md#networking-limits) 을 참조하세요.
