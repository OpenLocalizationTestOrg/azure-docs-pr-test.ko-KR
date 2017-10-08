---
title: "네트워크 감시자 aaaIntroduction tooAzure | Microsoft Docs"
description: "이 페이지에서는 hello 모니터링에 대 한 네트워크 감시자 서비스의 개요를 제공 하 고 형상화 네트워크는 Azure의 리소스에 연결"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 14bc2266-99e3-42a2-8d19-bd7257fec35e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 283b3fa6add05d9bad6d5dbdae1524344d1bfc7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-monitoring-overview"></a>Azure 네트워크 모니터링 개요

고객은 VNet, ExpressRoute, Application Gateway, 부하 분산 장치 등과 같은 다양한 개별 네트워크 리소스를 오케스트레이션하고 구성하여 Azure에서 종단 간 네트워크를 구축합니다. 모니터링 하는 것은 각 hello 네트워크 리소스에 사용할 수 있습니다. 리소스 수준 모니터링으로 모니터링 toothis 이라고 합니다.

복잡 한 구성 및 리소스를 만드는 시나리오 기반 네트워크 감시자를 통해 모니터링 해야 하는 복잡 한 시나리오 간의 상호 작용 hello 엔드 tooend 네트워크를 가질 수 있습니다.

이 문서에서는 시나리오 및 리소스 수준 모니터링에 대해 설명합니다. Azure의 네트워크 모니터링은 포괄적이며 다음 두 가지 범주를 포함합니다.

* [**네트워크 감시자** ](#network-watcher) -모니터링 시나리오 기반 네트워크 감시자의 hello 기능과 함께 제공 됩니다. 이 서비스에는 패킷 캡처, 다음 홉, IP 흐름 확인, 보안 그룹 보기, NSG 흐름 로그가 포함되어 있습니다. 수준 모니터링 시나리오는 전체적인 tooend 뷰 대비 tooindividual 네트워크 리소스 모니터링의 네트워크 리소스를 제공합니다.
* [**리소스 모니터링**](#network-resource-level-monitoring) - 리소스 수준 모니터링은 진단 로그, 메트릭, 문제 해결 및 리소스 상태의 네 가지 기능으로 구성됩니다. 이러한 모든 기능은 hello 네트워크 리소스 수준에서 빌드됩니다.

## <a name="network-watcher"></a>Network Watcher

네트워크 감시자는 toomonitor 있습니다 수 있도록 하는 지역 서비스 및 네트워크 시나리오의 수준에서 및 Azure에서 상태를 진단 합니다. 네트워크 문제 진단 및 시각화 도구를 사용할 수 있는 네트워크 감시자 insights tooyour Azure 네트워크에에서 가져오고 이해, 진단, 하는 데 도움이 됩니다.

네트워크 감시자는 현재 hello 기능 뒤에 있습니다.

* **[토폴로지](network-watcher-topology-overview.md)**  -다양 한 상호 연결 및 연결 된 리소스 그룹에에서 네트워크 리소스 간에 네트워크 개요 표시 된 hello를 제공 합니다.
* **[변수 패킷 캡처](network-watcher-packet-capture-overview.md)** - 가상 컴퓨터의 내부 및 외부 패킷 데이터를 캡처합니다. 고급 필터링 옵션 및 수 tooset 시간 예 세밀 하 게 컨트롤 크기 제한 다양 한 기능을 제공 합니다. blob 저장소에 또는 로컬 디스크에.cap 형식 hello hello 패킷 데이터를 저장할 수 있습니다.
* **[IP 흐름 확인](network-watcher-ip-flow-verify-overview.md)** - 흐름 정보의 5개 튜플 패킷 매개 변수(대상 IP, 원본 IP, 대상 포트, 원본 포트 및 프로토콜)에 따라 패킷을 허용하거나 거부하는지 확인합니다. Hello 패킷 보안 그룹에 의해 거부 되 면 hello 규칙과 hello 패킷 거부 그룹 반환 됩니다.
* **[다음 홉](network-watcher-next-hop-overview.md)**  -hello toodiagnose 잘못 구성 된 모든 사용자 정의 경로 사용 하면 Azure 네트워크 패브릭에서 라우팅되는 패킷의 hello 다음 홉을 결정 합니다.
* **[보안 그룹 보기](network-watcher-security-group-view-overview.md)**  -VM에 적용 되는 hello 효과적이 고 적용 된 보안 규칙을 가져옵니다.
* **[NSG 흐름 로깅](network-watcher-nsg-flow-logging-overview.md)**  -네트워크 보안 그룹에 대 한 흐름 로그 허용 되거나 hello hello 그룹 보안 규칙에 의해 거부 된 toocapture 로그 관련된 tootraffic를 사용 합니다. hello 흐름은 5-튜플 정보 – 원본 IP, 대상 IP, 원본 포트, 대상 포트 및 프로토콜에 의해 정의 됩니다.
* **[가상 네트워크 게이트웨이 및 연결 문제 해결](network-watcher-troubleshoot-manage-rest.md)**  -hello 기능 tootroubleshoot 제공 가상 네트워크 게이트웨이 및 연결 합니다.
* **[구독 제한 네트워크](#network-subscription-limits)**  -제한에 대해 tooview 네트워크 리소스 사용을 활성화 합니다.
* **[진단 로그 구성](#diagnostic-logs)**  – 단일 창 tooenable 제공 하거나 리소스 그룹의 네트워크 리소스에 대 한 진단 로그를 사용 하지 않도록 설정 합니다.
* **[연결 (미리 보기)](network-watcher-connectivity-overview.md)**  -끝점을 제공 하는 가상 컴퓨터 tooa의 직접 TCP 연결을 설정 하는 hello 가능성을 확인 합니다.

### <a name="role-based-access-control-rbac-in-network-watcher"></a>Network Watcher의 RBAC(역할 기반 액세스 제어)

네트워크 감시자 hello를 사용 하 여 [신속히 알아봅니다 액세스 제어 (RBAC) 모델](../active-directory/role-based-access-control-what-is.md)합니다. 네트워크 감시자 hello 다음 권한을 hello가 필요 합니다. 네트워크 감시자를 사용 하 여 hello 포털에서 또는 네트워크 감시자 Api 시작에 사용 되는 해당 hello 역할에 필요한 hello 액세스 권한이 있는지 중요 toomake 것 합니다.

|리소스| 사용 권한|
|---|---| 
|Microsoft.Storage/ |읽기|
|Microsoft.Authorization/| 읽기| 
|Microsoft.Resources/subscriptions/resourceGroups/| 읽기|
|Microsoft.Storage/storageAccounts/listServiceSas/ | 작업|
|Microsoft.Storage/storageAccounts/listAccountSas/ |작업|
|Microsoft.Storage/storageAccounts/listKeys/ | 작업|
|Microsoft.Compute/virtualMachines/ |읽기|
|Microsoft.Compute/virtualMachines/ |쓰기|
|Microsoft.Compute/virtualMachineScaleSets/ |읽기|
|Microsoft.Compute/virtualMachineScaleSets/ |쓰기|
|Microsoft.Network/networkWatchers/packetCaptures/ |읽기|
|Microsoft.Network/networkWatchers/packetCaptures/| 쓰기|
|Microsoft.Network/networkWatchers/packetCaptures/| 삭제|
|Microsoft.Network/networkWatchers/ |쓰기 |
|Microsoft.Network/networkWatchers/| 읽기 |
|Microsoft.Insights/alertRules/ |*|
|Microsoft.Support/ | *|

### <a name="network-subscription-limits"></a>네트워크 구독 제한

네트워크의 구독 제한 hello 사용할 수 있는 리소스의 최대 수와 지역에서 구독에 hello 네트워크 리소스의 각 hello 사용량의 세부 정보를 제공합니다.

![네트워크 구독 제한][nsl]

## <a name="network-resource-level-monitoring"></a>네트워크 리소스 수준 모니터링

같은 기능 hello 리소스 수준 모니터링을 위해 사용할 수 있습니다.

### <a name="audit-log"></a>감사 로그

네트워크의 hello 구성의 일부분으로 수행 되는 작업 기록 됩니다. 이러한 로그는 hello Azure 포털에서에서 볼 수 있습니다 또는 Power BI와 같은 Microsoft 도구 또는 타사 도구를 사용 하 여 검색 합니다. 감사 로그는 hello 포털, PowerShell, CLI 및 Rest API를 통해 사용할 수 있습니다. 감사 로그에 대한 자세한 내용은 [Resource Manager를 사용하는 감사 작업](../resource-group-audit.md)을 참조하세요.

감사 로그는 모든 네트워크 리소스에서 수행된 작업에 사용할 수 있습니다.

### <a name="metrics"></a>메트릭

메트릭은 일정 기간 동안 수집된 성능 측정 및 카운터입니다. 메트릭은 현재 Application Gateway에서 사용할 수 있습니다. 메트릭은은 tootrigger 사용 되는 경고 임계값에 기반을 수 있습니다. 참조 [응용 프로그램 게이트웨이 진단](../application-gateway/application-gateway-diagnostics.md) tooview 어떻게 메트릭을 사용 하는 toocreate 경고 수입니다.

![메트릭 보기][metrics]

### <a name="diagnostic-logs"></a>진단 로그

정기적이 고 비 정기적인 이벤트는 네트워크 리소스에 의해 생성 및 tooan 이벤트 허브 또는 로그 분석을 전송 하는 저장소 계정에 기록 됩니다. 이러한 로그는 리소스의 hello 상태에 대 한 정보를 제공합니다. Power BI 및 Log Analytics와 같은 도구에서 볼 수 있습니다. tooview 진단 로그를 방문 하는 방법을 toolearn [로그 분석](../log-analytics/log-analytics-azure-networking-analytics.md)합니다.

진단 로그는 [부하 분산 장치](../load-balancer/load-balancer-monitor-log.md), [네트워크 보안 그룹](../virtual-network/virtual-network-nsg-manage-log.md), 경로 및 [Application Gateway](../application-gateway/application-gateway-diagnostics.md)에서 사용할 수 있습니다.

Network Watcher는 진단 로그 보기를 제공합니다. 이 보기에는 진단 로깅을 지원하는 모든 네트워킹 리소스가 포함됩니다. 이 보기에서 네트워킹 리소스를 빠르고 편리하게 사용하거나 사용하지 않도록 설정할 수 있습니다.

![로그][logs]

### <a name="troubleshooting"></a>문제 해결

hello 블레이드에서 hello 포털에서 환경 문제 해결에 제공 됩니다 네트워크 리소스 오늘 개별 리소스와 관련 된 toodiagnose 일반적인 문제. 이 환경은 다음 네트워크 리소스-ExpressRoute, VPN 게이트웨이, 응용 프로그램 게이트웨이, 네트워크 보안 로그, 경로, DNS, 부하 분산 장치 및 트래픽 관리자는 hello에 대 한 ´ ù. toolearn 수준 문제 해결 리소스에 대 한 방문 [Azure 문제 해결 된 문제를 진단 및 해결](https://azure.microsoft.com/blog/azure-troubleshoot-diagonse-resolve-issues/)

![문제 해결 정보][TS]

### <a name="resource-health"></a>리소스 상태

네트워크 리소스의 hello 상태는 주기적으로 제공 됩니다. 이러한 리소스에는 VPN Gateway 및 VPN 터널이 포함됩니다. 리소스 상태는 hello Azure 포털에서 액세스할 수 있습니다. 리소스 상태에 대해 자세히 toolearn 방문 [리소스 상태 개요](../resource-health/resource-health-overview.md)

## <a name="next-steps"></a>다음 단계

Network Watcher에 대해 알아보았으면 다음을 익힐 수 있습니다.

방문 하 여 VM에 패킷 캡처를 수행할 [hello Azure 포털에서에서 변수 패킷 캡처](network-watcher-packet-capture-manage-portal.md)

[경고로 인해 발생한 패킷 캡처](network-watcher-alert-triggered-packet-capture.md)를 사용하여 자동 관리 모니터링 및 진단을 수행합니다.

오픈 소스 도구를 사용하는 [Wireshark로 패킷 캡처 분석](network-watcher-deep-packet-inspection.md)을 통해 보안 취약점을 감지합니다.

일부 hello에 대 한 자세한 내용은 다른 키 [네트워킹 기능](../networking/networking-overview.md) Azure의 합니다.

<!--Image references-->
[TS]: ./media/network-watcher-monitoring-overview/troubleshooting.png
[logs]: ./media/network-watcher-monitoring-overview/logs.png
[metrics]: ./media/network-watcher-monitoring-overview/metrics.png
[nsl]: ./media/network-watcher-monitoring-overview/nsl.png











