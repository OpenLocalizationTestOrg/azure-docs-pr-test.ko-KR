---
title: "aaaTroubleshoot 연결할 수 없는 Azure 사이트 간 VPN 연결 | Microsoft Docs"
description: "자세한 내용은 어떻게 tootroubleshoot 사이트 간 VPN 연결 하는 갑자기 작동을 중단 하 고 다시 연결할 수 없습니다."
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
ms.openlocfilehash: 632c75bfcfb93a532eeead2855d43e6614569a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a>문제 해결: Azure 사이트 간 VPN 연결에서 연결할 수 없고 작동이 중지됨

온-프레미스 네트워크와 Azure 가상 네트워크 간의 사이트 간 VPN 연결을 구성한 후 hello VPN 연결 갑자기 작동을 중지 하 고 다시 연결할 수 없습니다. 이 문서에서는 문제 해결 단계 toohelp이이 문제를 해결 합니다. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a>문제 해결 단계

tooresolve hello 문제를 먼저 시도 합니다. 너무[재설정 hello Azure VPN 게이트웨이](vpn-gateway-resetgw-classic.md) hello 터널 hello 온-프레미스 VPN 장치를 다시 설정 합니다. Hello 문제가 계속 되 면 hello 문제 중 해당 단계 tooidentify hello 인해를 수행 합니다.

### <a name="prerequisite-step"></a>필수 조건 단계

Hello hello Azure VPN 게이트웨이 유형을 확인 합니다.

1. Toohello 이동 [Azure 포털](https://portal.azure.com)합니다.

2. Hello 확인 **개요** hello 형식 정보에 대 한 hello VPN 게이트웨이의 페이지입니다.
    
    ![Hello 게이트웨이 개요](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a>1단계. Hello 온-프레미스 VPN 장치의 유효성을 검사 하는지 확인 하십시오.

1. [확인된 VPN 장치 및 운영 체제 버전](vpn-gateway-about-vpn-devices.md#devicetable)을 사용 중인지 확인합니다. 유효성이 검사 된 VPN 장치 hello 장치가 아닌 경우 호환성 문제가 있는 경우 toocontact hello 장치 제조업체 toosee를 할 수 있습니다.

2. 해당 hello VPN 장치가 올바르게 구성 되어 있는지 확인 합니다. 자세한 내용은 [장치 구성 예제 편집](/vpn-gateway-about-vpn-devices.md#editing)을 참조하세요.

### <a name="step-2-verify-hello-shared-key"></a>2단계. Hello 공유 키를 확인 합니다.

Hello hello 온-프레미스 VPN 장치 toohello Azure 가상 네트워크 VPN toomake hello 키와 일치 하는지에 대 한 공유 키를 비교 합니다. 

hello tooview hello Azure VPN 연결에 대 한 공유 키를 사용 하 여 hello 메서드를 다음 중 하나:

**Azure 포털**

1. 만든 toohello VPN 게이트웨이 사이트 간 연결을 이동 합니다.

2. Hello에 **설정** 섹션에서 클릭 **공유 키**합니다.
    
    ![공유 키](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

**Azure PowerShell**

Hello Azure 리소스 관리자 배포 모델:

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

Hello 클래식 배포 모델:

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-hello-vpn-peer-ips"></a>3단계. Hello VPN 피어 Ip 확인

-   hello에 IP 정의 hello **로컬 네트워크 게이트웨이** 개체 Azure의 hello 온-프레미스 장치 IP와 일치 해야 합니다.
-   hello Azure 게이트웨이 IP 정의 hello에 설정 된 온-프레미스 장치에는 hello Azure 게이트웨이 IP와 일치 해야 합니다.

### <a name="step-4-check-udr-and-nsgs-on-hello-gateway-subnet"></a>4단계. Hello 게이트웨이 서브넷에 Nsg 및 UDR 확인

에 대 한 확인 하 고 hello 게이트웨이 서브넷에 라우팅 사용자 정의 (UDR) 또는 (Nsg) 네트워크 보안 그룹을 제거 하 고 hello 결과 테스트 합니다. Hello 문제가 해결 되 면 hello 설정을 적용 UDR 또는 NSG의 유효성을 검사 합니다.

### <a name="step-5-check-hello-on-premises-vpn-device-external-interface-address"></a>5단계. Hello 온-프레미스 VPN 장치 외부 인터페이스 주소를 확인 합니다.

- Hello hello VPN 장치의 인터넷 연결 IP 주소는 hello에 포함 되어 있으면 **로컬 네트워크** 정의 Azure에서 산발적 연결 끊김 발생할 수 있습니다.
- hello 장치 외부 인터페이스 해야 hello 인터넷에서 직접 합니다. 네트워크 주소 변환 또는 인터넷 hello 및 hello 장치 사이 방화벽이 없습니다 있어야 합니다.
- tooconfigure 방화벽 클러스터링 toohave 가상 IP hello 클러스터를 중단 하 고 tooa 공용 인터페이스는 hello 게이트웨이 수와 상호 작용할 직접 hello VPN 어플라이언스를 노출 해야 합니다.

### <a name="step-6-verify-that-hello-subnets-match-exactly-azure-policy-based-gateways"></a>6단계. Hello 서브넷 정확히 일치 하는지 확인 하십시오 (정책 기반 Azure 게이트웨이)

-   Hello 서브넷 hello Azure 가상 네트워크와 Azure 가상 네트워크 hello에 대 한 온-프레미스 정의 간에 정확히 일치 하는지 확인 합니다.
-   Hello 서브넷 hello 간에 정확히 일치 하는지 확인 **로컬 네트워크 게이트웨이** 및 온-프레미스 hello 온-프레미스 네트워크에 대 한 정의입니다.

### <a name="step-7-verify-hello-azure-gateway-health-probe"></a>7단계. Hello Azure 게이트웨이 상태 프로브를 확인 합니다.

1. Toohello 이동 [상태 프로브](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe)합니다.

2. Hello 인증서 경고를 클릭 합니다.
3. 응답을 수신 하는 경우 hello VPN 게이트웨이 정상인 상태로 간주 됩니다. 응답을 수신 하지 않는 hello 게이트웨이 정상 수 없거나 hello 게이트웨이 서브넷에 NSG hello 문제가 발생 합니다. hello 텍스트 다음은 샘플 응답:

    &lt;?xml version="1.0"?>  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">기본 인스턴스: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;

### <a name="step-8-check-whether-hello-on-premises-vpn-device-has-hello-perfect-forward-secrecy-feature-enabled"></a>8단계: 여부 hello 온-프레미스 VPN 장치에 hello 전달 완전 기능 사용 확인

hello 전달 완전 기능에는 연결을 끊는 문제가 발생할 수 있습니다. Hello VPN 장치 활성화 전달 완전 있으면 hello 기능을 사용 하지 않도록 설정 합니다. Hello VPN 게이트웨이 IPsec 정책을 업데이트 합니다.

## <a name="next-steps"></a>다음 단계

-   [사이트 간 연결 tooa 가상 네트워크 구성](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [사이트 간 VPN 연결에 대한 IPsec/IKE 정책 구성](vpn-gateway-ipsecikepolicy-rm-powershell.md)
