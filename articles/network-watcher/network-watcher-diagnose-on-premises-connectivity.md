---
title: "네트워크 감시자 Azure VPN 게이트웨이 통해 온-프레미스 연결과 aaaDiagnose | Microsoft Docs"
description: "이 문서에서는 어떻게 toodiagnose 온-프레미스 Azure 네트워크 감시자 리소스 문제 해결에 대 한 VPN 게이트웨이 통해 연결을 설명 합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: aeffbf3d-fd19-4d61-831d-a7114f7534f9
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 9941c5d1b49bec29062210684dae8653cbdb84b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-on-premises-connectivity-via-vpn-gateways"></a>VPN Gateway를 통한 온-프레미스 연결 진단

Azure VPN 게이트웨이 온-프레미스 네트워크와 Azure 가상 네트워크 간의 보안 연결에 대 한 hello 요구를 해결 하는 toocreate 하이브리드 솔루션이 있습니다. 요구 사항에이 고유 하므로 온-프레미스 VPN 장치의 hello 선택 하므로입니다. Azure는 현재 지원 [여러 VPN 장치](../vpn-gateway/vpn-gateway-about-vpn-devices.md#devicetable) hello 장치 공급 업체와 협력에서 유효성이 검사 계속 됩니다. 온-프레미스 VPN 장치를 구성 하기 전에 hello 장치 관련 구성 설정을 검토 합니다. 마찬가지로 Azure VPN Gateway는 연결을 설정하는 데 사용되는 [지원되는 IPsec 매개 변수](../vpn-gateway/vpn-gateway-about-vpn-devices.md#ipsec)의 집합으로 구성됩니다. 현재 toospecify 또는 hello Azure VPN 게이트웨이에서 IPsec 매개 변수의 특정 조합 선택 방법이 있습니다. 온-프레미스와 Azure 간에 성공적으로 연결을 설정 하기 위한 hello 온-프레미스 VPN 장치 설정을 hello IPsec 매개 변수 Azure VPN 게이트웨이에 규정을 준수 해야 합니다. 경우 hello 설정 된 올바른, 연결 끊김 않으며 지금까지 이러한 문제 해결 trivial 되었으며 보통 tooidentify 및 수정 프로그램 hello 문제 몇 시간입니다.

Hello Azure 네트워크 감시자로 기능, 해결 있습니다 수 toodiagnose 게이트웨이 및 연결 문제를 되며 분 이내 사용할 충분 한 정보 toomake 결정을 내릴된 toorectify hello 문제입니다.

## <a name="scenario"></a>시나리오

Azure 및 온-프레미스 간 tooconfigure 사이트-사이트 연결을 원하는 대로 hello 온-프레미스 VPN 게이트웨이 FortiGate를 사용 하 여 합니다. tooachieve이이 시나리오에서는 다음과 같은 설정이 hello 필요 합니다.

1. 가상 네트워크 게이트웨이 hello Azure에서 VPN 게이트웨이
1. 로컬 네트워크 게이트웨이-hello [온-프레미스 (FortiGate) VPN 게이트웨이](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) Azure 클라우드에서 표현
1. 사이트 간 연결 (정책 기반)- [hello VPN 게이트웨이 및 hello 간의 연결 온-프레미스 라우터](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md#createconnection)
1. [FortiGate 구성](https://github.com/Azure/Azure-vpn-config-samples/blob/master/Fortinet/Current/Site-to-Site_VPN_using_FortiGate.md)

방문 하 여 구성 사이트 간 구성에 대 한 자세한 단계별 지침을 찾을 수 있습니다: [hello Azure 포털을 사용 하 여 사이트 간 연결이 포함 된 VNet을 만들](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)합니다.

Hello IPsec 통신 매개 변수를 구성 하는 hello 중요 한 구성 단계 중 하나, 모든 잘못 된 구성을 hello 온-프레미스 네트워크와 Azure 간의 연결 tooloss 이어집니다. 현재 Azure VPN 게이트웨이 1 단계에 대 한 IPsec 매개 변수를 따라 구성 된 toosupport hello. 앞에서 언급했듯이 이러한 설정은 수정할 수 없습니다.  Hello 테이블 아래에 보시 Azure VPN 게이트웨이에서 지원 hello 암호화 알고리즘은 AES256, AES128, 및 3DES를 사용 합니다.

### <a name="ike-phase-1-setup"></a>IKE 1단계 설정

| **속성** | **정책 기반** | **경로 기반 및 표준 또는 고성능 VPN Gateway** |
| --- | --- | --- |
| IKE 버전 |IKEv1 |IKEv2 |
| Diffie-Hellman 그룹 |그룹 2(1024비트) |그룹 2(1024비트) |
| 인증 방법 |미리 공유한 키 |미리 공유한 키 |
| 암호화 알고리즘 |AES256 AES128 3DES |AES256 (3DES) |
| 해시 알고리즘 |SHA1(SHA128) |SHA1(SHA128), SHA2(SHA256) |
| 1단계 SA(보안 연결) 수명(시간) |28,800초 |10,800초 |

사용자로 필요한 tooconfigure 것 프로그램 FortiGate 샘플 구성에서 찾을 수 있습니다 [GitHub](https://github.com/Azure/Azure-vpn-config-samples/blob/master/Fortinet/Current/fortigate_show%20full-configuration.txt)합니다. 자신도 모르는 사이 hello 해시 알고리즘으로 프로그램 FortiGate toouse s h A-512를 구성 합니다. 이 알고리즘은 정책 기반 연결에 대해 지원되는 알고리즘이 아니므로 VPN 연결이 작동합니다.

이러한 문제는 하드 tootroubleshoot 않으며 근본 원인을 비 직관적 경우가 많습니다. 이 경우 hello 문제 해결에 지원 티켓 tooget 도움말을 열 수 있습니다. 그러나 Azure Network Watcher 문제 해결 API를 사용하면 이러한 문제를 직접 식별할 수 있습니다.

## <a name="troubleshooting-using-azure-network-watcher"></a>Azure Network Watcher를 사용하여 문제 해결

toodiagnose 해당 연결을 tooAzure PowerShell 연결 및 시작 hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet. 이 cmdlet을 사용 하 여에 hello 세부 정보를 찾을 수 있습니다 [가상 네트워크 게이트웨이 문제 해결 및 연결-PowerShell](network-watcher-troubleshoot-manage-powershell.md)합니다. 이 cmdlet은 toofew 분 toocomplete를 차지할 수 있습니다.

Hello cmdlet이 완료 되 면 hello cmdlet에 지정 된 toohello 저장소 위치를 탐색할 수 있습니다 tooget에 hello 문제 및 로그에 대 한 정보를 자세히 합니다. Azure 네트워크 감시자 hello 다음 로그 파일이 포함 된 zip 폴더를 만듭니다.

![1][1]

IKEErrors.txt 및 그 열기 hello 파일 표시 hello 다음 오류 메시지가 표시 문제를 온-프레미스 IKE 설정 잘못 구성 합니다.

```
Error: On-premises device rejected Quick Mode settings. Check values.
     based on log : Peer sent NO_PROPOSAL_CHOSEN notify
```

이 경우에 대해 언급 있었다는 것 처럼 hello Scrubbed wfpdiag.txt hello 오류에 대 한에서 자세한 정보를 얻을 수 있습니다 `ERROR_IPSEC_IKE_POLICY_MATCH` 해당 리드 tooconnection 제대로 작동 하지 않습니다.

또 다른 일반적인 구성 오류는 잘못 된 공유 키를 지정 하는 hello입니다. 이전 예제에서는 서로 다른 공유 키에 지정한 hello에 있는 경우 IKEErrors.txt hello 다음 오류가 hello: `Error: Authentication failed. Check shared key`합니다.

Azure 네트워크 감시자 기능 문제를 해결 하면 toodiagnose 수 있으며 간단한 PowerShell cmdlet의 hello 쉽도록 VPN 게이트웨이 및 연결 문제를 해결 합니다. 현재 조건에 따라 진단 hello를 지원 하 고 더 많은 조건 추가 대해 작동 합니다.

### <a name="gateway"></a>게이트웨이

| 오류 유형 | 이유 | 로그|
|---|---|---|
| NoFault | 오류가 발견되지 않은 경우를 나타냅니다. |예|
| GatewayNotFound | 게이트웨이를 찾을 수 없거나 게이트웨이가 프로비저닝되지 않았습니다. |아니요|
| PlannedMaintenance |  게이트웨이 인스턴스가 유지 관리되고 있습니다.  |아니요|
| UserDrivenUpdate | 사용자 업데이트를 진행 중인 경우를 나타냅니다. 크기 조정 작업일 수 있습니다. | 아니요 |
| VipUnResponsive | Hello hello 게이트웨이의 기본 인스턴스를 연결할 수 없습니다. 이 hello 상태 검색에 실패할 때 발생 합니다. | 아니요 |
| PlatformInActive | Hello 플랫폼에 문제가 있습니다. | 아니요|
| ServiceNotRunning | hello 기본 서비스가 실행 되지 않습니다. | 아니요|
| NoConnectionsFoundForGateway | 연결이 없는 hello 게이트웨이에 있습니다. 단지 경고일 뿐입니다.| 아니요|
| ConnectionsNotConnected | Hello 연결 없음 연결 됩니다. 단지 경고일 뿐입니다.| 예|
| GatewayCPUUsageExceeded | hello 현재 게이트웨이 사용량 CPU 사용량은 > 95%입니다. | 예 |

### <a name="connection"></a>연결

| 오류 유형 | 이유 | 로그|
|---|---|---|
| NoFault | 오류가 발견되지 않은 경우를 나타냅니다. |예|
| GatewayNotFound | 게이트웨이를 찾을 수 없거나 게이트웨이가 프로비저닝되지 않았습니다. |아니요|
| PlannedMaintenance | 게이트웨이 인스턴스가 유지 관리되고 있습니다.  |아니요|
| UserDrivenUpdate | 사용자 업데이트를 진행 중인 경우를 나타냅니다. 크기 조정 작업일 수 있습니다.  | 아니요 |
| VipUnResponsive | Hello hello 게이트웨이의 기본 인스턴스를 연결할 수 없습니다. Hello 상태 검색이 실패 하면 발생 합니다. | 아니요 |
| ConnectionEntityNotFound | 연결 구성이 없습니다. | 아니요 |
| ConnectionIsMarkedDisconnected | "연결이 끊어졌습니다." hello 연결 표시 |아니요|
| ConnectionNotConfiguredOnGateway | hello 기본 서비스 연결을 구성 하는 hello를 않아도 됩니다. | 예 |
| ConnectionMarkedStandy | 기본 서비스가 hello 대기로 표시 되어 있습니다.| 예|
| 인증 | 미리 공유한 키가 일치하지 않습니다. | 예|
| PeerReachability | hello 피어 게이트웨이 연결할 수 없습니다. | 예|
| IkePolicyMismatch | hello 피어 게이트웨이 Azure에서 지원 되지 않는 IKE 정책에 있습니다. | 예|
| WfpParse 오류 | Hello WFP 로그 구문 분석 오류가 있습니다. |예|

## <a name="next-steps"></a>다음 단계

방문 하 여 PowerShell 및 Azure 자동화의 toocheck VPN 게이트웨이 연결에 알아봅니다 [Azure 네트워크 감시자 문제 해결 모니터 VPN 게이트웨이](network-watcher-monitor-with-azure-automation.md)

[1]: ./media/network-watcher-diagnose-on-premises-connectivity/figure1.png
