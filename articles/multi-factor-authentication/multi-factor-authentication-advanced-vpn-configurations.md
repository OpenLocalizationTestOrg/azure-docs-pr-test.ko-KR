---
title: "Azure MFA와 타사 Vpn aaaAdvanced 시나리오"
description: "Cisco, Citrix, Juniper와 toointegrate Azure MFA에 대 한 단계별 구성 가이드입니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1f94a214-d6f6-48a8-8a12-006b5896ae45
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/13/2017
ms.author: kgremban
ms.openlocfilehash: e23960ca4977cc01271f99fa2bec70449e9acfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-scenarios-with-azure-multi-factor-authentication-and-third-party-vpn-solutions"></a>Azure Multi-Factor Authentication 및 타사 VPN 솔루션을 사용한 고급 시나리오
Azure Multi-factor Authentication을 사용할 수 있습니다 tooseamlessly 다양 한 타사 VPN 솔루션을 사용 하 여 연결 합니다. 이 문서는 Cisco® ASA VPN 어플라이언스, Citrix NetScaler SSL VPN 어플라이언스 및 hello Juniper 네트워크 보안 액세스/Pulse Secure 연결 보안 SSL VPN 어플라이언스를 중점적으로 수행 합니다. 이러한 세 가지 일반적인 어플라이언스 구성 가이드 tooaddress 만든 하지만 Multi-factor Authentication 서버 RADIUS, LDAP, IIS, 또는 클레임 기반 인증 tooAD FS 사용 하는 대부분 시스템을 통합할 수 있습니다. [MFA 서버 구성](multi-factor-authentication-get-started-server.md#next-steps)에서 자세한 내용을 볼 수 있습니다.

## <a name="cisco-asa-vpn-appliance-and-azure-multi-factor-authentication"></a>Cisco ASA VPN 어플라이언스 및 Azure Multi-Factor Authentication
Azure Multi-factor Authentication Cisco AnyConnect® VPN 로그인 및 포털 액세스에 대 한 Cisco® ASA VPN 어플라이언스 tooprovide 추가 보안 통합합니다.  이렇게 하려면 두 hello LDAP 또는 RADIUS 프로토콜을 사용 하 여 합니다.  Hello toodownload hello 자세한 단계별 구성 다음 중 하나를 선택 과정을 안내 합니다.

| 구성 가이드 | 설명 |
| --- | --- |
| [Anyconnect VPN을 사용한 Cisco ASA 및 LDAP를 위한 Azure MFA 구성](http://download.microsoft.com/download/A/2/0/A201567C-C3DE-4227-AF89-4567A470899E/Cisco_ASA_Azure_MFA_LDAP.docx) | LDAP를 사용하는 Azure MFA와 Cisco ASA VPN 어플라이언스 통합 |
| [Anyconnect VPN을 사용한 Cisco ASA 및 RADIUS를 위한 Azure MFA 구성](http://download.microsoft.com/download/4/5/7/4579C1CF-35B0-4FBE-8A1A-B49CB2CC0382/Cisco_ASA_Azure_MFA_RADIUS.docx) | RADIUS를 사용하는 Azure MFA와 Cisco ASA VPN 어플라이언스 통합 |

## <a name="citrix-netscaler-ssl-vpn-and-azure-multi-factor-authentication"></a>Citrix NetScaler SSL VPN 및 Azure Multi-Factor Authentication
Azure Multi-factor Authentication Citrix NetScaler SSL VPN 로그인 및 포털 액세스에 대 한 Citrix NetScaler SSL VPN 어플라이언스 tooprovide 추가 보안 통합합니다.  이렇게 하려면 두 hello LDAP 또는 RADIUS 프로토콜을 사용 하 여 합니다.  Hello toodownload hello 자세한 단계별 구성 다음 중 하나를 선택 과정을 안내 합니다.

| 구성 가이드 | 설명 |
| --- | --- |
| [Citrix NetScaler SSL VPN 및 LDAP를 위한 Azure MFA 구성](http://download.microsoft.com/download/2/4/E/24E1E722-72DF-471F-A88A-D1338DB1AF83/Citrix_NS_Azure_MFA_LDAP.docx) | LDAP를 사용하는 Azure MFA와 Citrix NetScaler SSL VPN 어플라이언스 통합 |
| [Citrix NetScaler SSL VPN 및 RADIUS를 위한 Azure MFA 구성](http://download.microsoft.com/download/1/A/4/1A482764-4A63-45C2-A5EC-2B673ACCDD12/Citrix_NS_Azure_MFA_RADIUS.docx) | RADIUS를 사용하는 Azure MFA와 Citrix NetScaler SSL VPN 어플라이언스 통합 |

## <a name="juniperpulse-secure-ssl-vpn-appliance-and-azure-multi-factor-authentication"></a>Juniper/Pulse Secure SSL VPN 어플라이언스 및 Azure Multi-Factor Authentication
Azure Multi-factor Authentication Juniper/Pulse Secure SSL VPN 로그인 및 포털 액세스에 대 한 Juniper/Pulse Secure SSL VPN 어플라이언스 tooprovide 추가 보안 통합합니다.  이렇게 하려면 두 hello LDAP 또는 RADIUS 프로토콜을 사용 하 여 합니다.  Hello toodownload hello 자세한 단계별 구성 다음 중 하나를 선택 과정을 안내 합니다.

| 구성 가이드 | 설명 |
| --- | --- |
| [Juniper/Pulse Secure SSL VPN 및 LDAP를 위한 Azure MFA 구성](http://download.microsoft.com/download/6/5/8/6587B418-75B1-4FCB-84D4-984BC479309E/JuniperPulse_Azure_MFA_LDAP.docx) | LDAP를 사용하는 Azure MFA와 Juniper/Pulse Secure SSL VPN 어플라이언스 통합 |
| [Juniper/Pulse Secure SSL VPN 및 RADIUS를 위한 Azure MFA 구성](http://download.microsoft.com/download/7/9/A/79AB3DAD-4799-4379-B1DA-B95ABDF231DC/JuniperPulse_Azure_MFA_RADIUS.docx) | RADIUS를 사용하는 Azure MFA와 Juniper/Pulse Secure SSL VPN 어플라이언스 통합 |

## <a name="next-steps"></a>다음 단계

- [Azure Multi-factor Authentication에 대 한 hello NPS 확장으로 기존 인증 인프라를 확장 합니다.](multi-factor-authentication-nps-extension.md)

- [Azure Multi-Factor Authentication 구성 설정](multi-factor-authentication-whats-next.md)