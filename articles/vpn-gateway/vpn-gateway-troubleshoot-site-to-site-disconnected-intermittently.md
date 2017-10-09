---
title: "Azure 사이트 간 VPN 연결이 일시적으로 끊어진 aaaTroubleshoot | Microsoft Docs"
description: "Tootroubleshoot 정기적으로 분리 하는 hello 사이트 간 VPN 연결에 문제가 hello 하는 방법에 대해 알아봅니다."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/21/2017
ms.author: genli
ms.openlocfilehash: 1ce3c4ff9d8f650312e45f33b760ebcc6597fc13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a>문제 해결: Azure 사이트 간 VPN 일시적 연결 끊김

새로운 또는 기존 Microsoft Azure 지점 및 사이트 간 VPN 연결 안정적이 지 않은 또는 정기적으로 연결을 끊습니다 hello 문제가 발생할 수 있습니다. 이 문서에서는 확인 하 고 hello 문제의 hello 원인을 해결 단계 toohelp 문제를 해결 합니다. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a>문제 해결 단계

### <a name="prerequisite-step"></a>필수 조건 단계

Azure 가상 네트워크 게이트웨이 hello 유형을 확인 합니다.

1. 너무 이동[Azure 포털](https://portal.azure.com)합니다.
2. Hello 확인 **개요** hello 형식 정보에 대 한 hello 가상 네트워크 게이트웨이의 페이지입니다.
    
    ![hello 게이트웨이의 hello 개요](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a>Hello 온-프레미스 VPN 장치의 유효성을 검사 하는지 여부를 1 단계

1. [확인된 VPN 장치 및 운영 체제 버전](vpn-gateway-about-vpn-devices.md#devicetable)을 사용 중인지 확인합니다. Hello VPN 장치 검증 되지 않은 경우에 모든 호환성 문제가 있는 경우 toocontact hello 장치 제조업체 toosee를 할 수 있습니다.
2. 해당 hello VPN 장치가 올바르게 구성 되어 있는지 확인 합니다. 자세한 내용은 [장치 구성 샘플 편집](vpn-gateway-about-vpn-devices.md#editing)을 참조하세요.

### <a name="step-2-check-hello-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a>2 단계 확인 hello 보안 연결 설정 (정책 기반 Azure 가상 네트워크 게이트웨이)

1. 확인 hello 가상 네트워크, 서브넷 및 범위 hello에 **로컬 네트워크 게이트웨이** 정의 Microsoft Azure의 hello 구성 hello 온-프레미스 VPN 장치에서와 같습니다.
2. Hello 보안 연결 설정을 일치 하는 확인 합니다.

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a>3단계 게이트웨이 서브넷에 대한 사용자 정의 경로 또는 네트워크 보안 그룹 확인

Hello 게이트웨이 서브넷의 사용자 정의 경로 사용 하는 일부 트래픽을 제한 하 고 다른 트래픽을 허용 될 수 있습니다. 이렇게 하면 일부 트래픽에 대 한 신뢰할 수 없는 및 다른 사용자에 대 한 좋은 hello VPN 연결 인지를 표시 합니다. 

### <a name="step-4-check-hello-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a>4 단계 확인 "서브넷 쌍 당 하나의 VPN 터널" hello (정책 기반 가상 네트워크 게이트웨이)에 대 한 설정

해당 hello 온-프레미스 VPN 장치가 toohave 설정 되어 있는지 확인 **서브넷 쌍 당 하나의 VPN 터널** 정책 기반 가상 네트워크 게이트웨이에 대 한 합니다.

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a>5단계 보안 연결 제한 확인(정책 기반 가상 네트워크 게이트웨이의 경우)

hello 정책 기반 가상 네트워크 게이트웨이 서브넷 보안 연결 쌍 200의 제한이 따릅니다. Azure 가상 네트워크 서브넷의 hello 수 번 곱한 hello로 로컬 서브넷의 수는 200 보다 크고, 연결 끊기 산발적 인 서브넷을 참조 하세요.

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a>6단계 온-프레미스 VPN 장치 외부 인터페이스 주소 확인

- Hello VPN 장치의 IP 주소를 사용 하는 인터넷 hello에 포함 되어 있으면 hello **로컬 네트워크 게이트웨이** 정의 Azure에서 산발적 연결 끊김 발생할 수 있습니다.
- hello 장치 외부 인터페이스 해야 hello 인터넷에서 직접 합니다. 네트워크 주소 변환 (NAT) 또는 인터넷 hello 및 hello 장치 사이 방화벽이 없습니다 있어야 합니다.
-  방화벽 클러스터링 toohave 가상 IP를 구성 하는 경우에 hello 클러스터를 중단 하 고 게이트웨이 hello tooa 공용 인터페이스와 상호 작용할 수 있는 직접 hello VPN 어플라이언스를 노출 해야 합니다.

### <a name="step-7-check-whether-hello-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a>Hello 온-프레미스 VPN 장치에 전달 완전 사용 여부를 7 확인 단계

hello **Perfect Forward Secrecy** 기능 hello 연결 끊기 문제가 발생할 수 있습니다. Hello VPN 장치에 있으면 **forward Secrecy 완벽 한** hello 기능을 해제를 사용 합니다. 그런 다음 [hello 가상 네트워크 게이트웨이 IPsec 정책 업데이트](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy)합니다.

## <a name="next-steps"></a>다음 단계

- [사이트 간 연결 tooa 가상 네트워크 구성](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [사이트 간 VPN 연결에 대한 IPsec/IKE 정책 구성](vpn-gateway-ipsecikepolicy-rm-powershell.md)

