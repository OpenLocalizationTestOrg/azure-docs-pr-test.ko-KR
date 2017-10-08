---
title: "방화벽 뒤에 있는 주요 자격 증명 모음 aaaAccess | Microsoft Docs"
description: "어떻게 tooaccess Azure 키 자격 증명 모음에서 방화벽 뒤에 있는 응용 프로그램에 대해 알아봅니다"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 50d21774-2ee1-4212-8995-570c9de603c5
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: ab4bb0c27a41fef878a20dace6cab203df04e579
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="access-azure-key-vault-behind-a-firewall"></a>방화벽 뒤에 있는 Azure Key Vault 액세스
### <a name="q-my-key-vault-client-application-needs-toobe-behind-a-firewall-what-ports-hosts-or-ip-addresses-should-i-open-tooenable-access-tooa-key-vault"></a>Q: 내 키 자격 증명 모음 클라이언트 응용 프로그램에는 방화벽 뒤에 있는 toobe가 필요 합니다. 어떤 포트, 호스트 또는 IP 주소 tooenable 액세스 tooa 주요 자격 증명 모음 열기 주의?
주요 자격 증명 모음 tooaccess 주요 자격 증명 모음 클라이언트 응용 프로그램에 tooaccess에 다양 한 기능에 대 한 여러 끝점:

* Azure AD(Azure Active Directory)를 통한 인증.
* Azure Key Vault의 관리. Azure Resource Manager를 통한 액세스 정책 만들기, 읽기, 업데이트, 삭제 및 설정을 포함합니다.
* 액세스 하 고 개체 (키 및 암호)에 저장 된 자격 증명 모음 키 자체를 관리, 키 자격 증명 모음 관련 끝점 hello를 진행 하 고 (예를 들어 [https://yourvaultname.vault.azure.net](https://yourvaultname.vault.azure.net)).  

구성 및 환경에 따라 일부의 변형이 있습니다.   

## <a name="ports"></a>포트
HTTPS를 통해 모든 트래픽을 tooa 주요 자격 증명 모음 세 함수 (인증, 관리 및 데이터 평면 액세스)는 모두에 대 한 라인: 포트 443입니다. 그러나 CRL의 경우 가끔 HTTP(포트 80) 트래픽이 있습니다. OCSP를 지원하는 클라이언트는 CRL에 도달하지 않아야 하지만 경우에 따라 [http://cdp1.public-trust.com/CRL/Omniroot2025.crl](http://cdp1.public-trust.com/CRL/Omniroot2025.crl)에 도달할 수 있습니다.  

## <a name="authentication"></a>인증
주요 자격 증명 모음 클라이언트 응용 프로그램 인증에 대 한 Azure Active Directory 끝점 tooaccess가 필요 합니다. Azure AD 테 넌 트 구성 hello에 사용 되는 hello 끝점은, hello 유형의 보안 주체 (사용자 계정 또는 서비스 사용자) 및 hello 유형의 계정-예를 들어 Microsoft 계정이 나 회사 또는 학교 계정을 합니다.  

| 주체 유형 | 끝점:포트 |
| --- | --- |
| Microsoft 계정을 사용하는 사용자<br> (예를 들어 user@hotmail.com) |**전역:**<br> login.microsoftonline.com:443<br><br> **Azure 중국:**<br> login.chinacloudapi.cn:443<br><br>**Azure 미국 정부:**<br> login-us.microsoftonline.com:443<br><br>**Azure 독일:**<br> login.microsoftonline.de:443<br><br> and <br>login.live.com:443 |
| 사용자 또는 Azure AD와 회사 또는 학교 계정을 사용 하 여 서비스 사용자 (예를 들어 user@contoso.com) |**전역:**<br> login.microsoftonline.com:443<br><br> **Azure 중국:**<br> login.chinacloudapi.cn:443<br><br>**Azure 미국 정부:**<br> login-us.microsoftonline.com:443<br><br>**Azure 독일:**<br> login.microsoftonline.de:443 |
| 사용자 또는 서비스 사용자는 회사 또는 학교 계정 및 Active Directory Federation Services (AD FS) 또는 다른 페더레이션된 끝점을 사용 하 여 (예를 들어 user@contoso.com) |회사 또는 학교 계정에 대한 모든 끝점 및 AD FS 또는 다른 페더레이션된 끝점 |

다른 복잡한 시나리오도 가능합니다. 너무 참조[Azure Active Directory 인증 흐름](/documentation/articles/active-directory-authentication-scenarios/), [Azure Active Directory와 응용 프로그램 통합](/documentation/articles/active-directory-integrating-applications/), 및 [Active Directory 인증 프로토콜](https://msdn.microsoft.com/library/azure/dn151124.aspx) 에 대 한 추가 정보입니다.  

## <a name="key-vault-management"></a>Key Vault 관리
주요 자격 증명 모음 관리 (CRUD 및 액세스 정책 설정), hello 주요 자격 증명 모음에 대 한 클라이언트 응용 프로그램 tooaccess Azure 리소스 관리자 끝점 필요 합니다.  

| 작업의 유형 | 끝점:포트 |
| --- | --- |
| 주요 자격 증명 모음 제어 평면 작업<br> Azure 리소스 관리자를 통해 |**전역:**<br> management.azure.com:443<br><br> **Azure 중국:**<br> management.chinacloudapi.cn:443<br><br> **Azure 미국 정부:**<br> management.usgovcloudapi.net:443<br><br> **Azure 독일:**<br> management.microsoftazure.de:443 |
| Azure Active Directory Graph API |**전역:**<br> graph.windows.net:443<br><br> **Azure 중국:**<br> graph.chinacloudapi.cn:443<br><br> **Azure 미국 정부:**<br> graph.windows.net:443<br><br> **Azure 독일:**<br> graph.cloudapi.de:443 |

## <a name="key-vault-operations"></a>Key Vault 작업
모든 주요 자격 증명 모음 개체 (키 및 암호) 관리 및 암호화 작업에 대 한 주요 자격 증명 모음 클라이언트 hello tooaccess hello 주요 자격 증명 모음 끝점이 필요합니다. hello 끝점 DNS 접미사는 주요 자격 증명 모음의 hello 위치에 따라 달라 집니다. hello 형식의 hello 주요 자격 증명 모음 끝점은 *자격 증명 모음 이름*. *특정 dns 접미사 지역*hello 표 다음에 설명 된 대로 합니다.  

| 작업의 유형 | 끝점:포트 |
| --- | --- |
| 키에 대한 암호화 작업을 포함하는 작업, 키 및 암호 만들기, 읽기, 업데이트 및 삭제, 키 자격 증명 모음 개체(키 또는 암호)의 태그 및 기타 특성 설정 또는 가져오기 |**전역:**<br> &lt;vault-name&gt;.vault.azure.net:443<br><br> **Azure 중국:**<br> &lt;vault-name&gt;.vault.azure.cn:443<br><br> **Azure 미국 정부:**<br> &lt;vault-name&gt;.vault.usgovcloudapi.net:443<br><br> **Azure 독일:**<br> &lt;vault-name&gt;.vault.microsoftazure.de:443 |

## <a name="ip-address-ranges"></a>IP 주소 범위
키 자격 증명 모음 서비스 hello PaaS 인프라 등의 다른 Azure 리소스를 사용합니다. 가능한 tooprovide 되기 때문 특정 IP 범위는 특정 시간에 서비스 끝점은 해당 주요 자격 증명 모음을 해결 합니다. 방화벽에만 IP 주소 범위를 지 원하는 경우 참조 toohello [Microsoft Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/details.aspx?id=41653) 문서. 인증 및 id (Azure Active Directory)에 대 한 응용 프로그램에 설명 된 수 tooconnect toohello 끝점 이어야 합니다 [인증 및 id 주소](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)합니다.

## <a name="next-steps"></a>다음 단계
주요 자격 증명 모음에 대 한 질문이 있으면 방문 hello [Azure 키 자격 증명 모음 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault)합니다.

