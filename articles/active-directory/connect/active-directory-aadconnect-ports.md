---
title: "포트 및 프로토콜이 필요한 하이브리드 ID - Azure | Microsoft Docs"
description: "이 페이지는 필요한 toobe Azure AD Connect에 대 한 열려 있는 포트에 대 한 기술 참조 페이지"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: de97b225-ae06-4afc-b2ef-a72a3643255b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: 9c62b74b45e7f266e3a55baa2db07a9ff1c9c6aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-identity-required-ports-and-protocols"></a>포트 및 프로토콜이 필요한 하이브리드 ID
다음 문서는 hello hello 필요한 포트 및 하이브리드 id 솔루션을 구현 하기 위한 프로토콜에 대 한 기술 참조입니다. 다음 그림 hello를 사용 하 고 toohello 해당 테이블을 참조 하십시오.

![Azure AD Connect의 정의](./media/active-directory-aadconnect-ports/required3.png)

## <a name="table-1---azure-ad-connect-and-on-premises-ad"></a>테이블 1 - Azure AD Connect 및 온-프레미스 AD
이 표에서 hello Azure AD Connect 서버 간의 통신에 필요한 hello 포트와 프로토콜 및 온-프레미스 AD.

| 프로토콜 | 포트 | 설명 |
| --- | --- | --- |
| DNS |53(TCP/UDP) |Hello 대상 포리스트에 DNS 조회 합니다. |
| Kerberos |88(TCP/UDP) |Kerberos 인증 toohello AD 포리스트 합니다. |
| MS-RPC |135(TCP/UDP) |Hello hello Azure AD Connect 마법사 toohello AD 포리스트를 바인딩할 때의 초기 구성 중 때와 암호 동기화를 사용 합니다. |
| LDAP |389(TCP/UDP) |AD에서 데이터를 가져오기 위해 사용합니다. 데이터가 Kerberos 서명 및 봉인으로 암호화됩니다. |
| RPC | 445(TCP/UDP) |원활한 SSO toocreate hello AD 포리스트의 컴퓨터 계정을 사용합니다. |
| LDAP/SSL |636(TCP/UDP) |AD에서 데이터를 가져오기 위해 사용합니다. hello 데이터 전송이 서명 되 고 암호화 합니다. SSL을 사용하는 경우에만 사용합니다. |
| RPC |49152- 65535(임의의 높은 RPC 포트)(TCP/UDP) |암호 동기화 및 hello toohello AD 포리스트를 바인딩할 때 Azure AD Connect의 초기 구성 중에 사용 합니다. 자세한 내용은 [KB929851](https://support.microsoft.com/kb/929851), [KB832017](https://support.microsoft.com/kb/832017) 및 [KB224196](https://support.microsoft.com/kb/224196)을 참조하세요. |

## <a name="table-2---azure-ad-connect-and-azure-ad"></a>테이블 2 - Azure AD Connect 및 Azure AD
이 표에서 hello Azure AD Connect 서버와 Azure AD 간의 통신에 필요한 hello 포트와 프로토콜을 설명 합니다.

| 프로토콜 | 포트 | 설명 |
| --- | --- | --- |
| HTTP |80(TCP/UDP) |Toodownload Crl (인증서 해지 목록) tooverify SSL 인증서를 사용 합니다. |
| HTTPS |443(TCP/UDP) |Azure AD와 toosynchronize 사용된 합니다. |

Url 및 IP 목록에 대 한 주소 tooopen 방화벽에 필요한 참조 [Office 365 Url 및 IP 주소 범위](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)합니다.

## <a name="table-3---azure-ad-connect-and-ad-fs-federation-serverswap"></a>테이블 3 - Azure AD Connect 및 AD FS 페더레이션 서버/WAP
이 표에서 hello 포트와 Azure AD Connect 서버 hello와 AD FS 페더레이션/WAP 서버 간의 통신에 필요한 프로토콜을 설명 합니다.  

| 프로토콜 | 포트 | 설명 |
| --- | --- | --- |
| HTTP |80(TCP/UDP) |Toodownload Crl (인증서 해지 목록) tooverify SSL 인증서를 사용 합니다. |
| HTTPS |443(TCP/UDP) |Azure AD와 toosynchronize 사용된 합니다. |
| WinRM |5985 |WinRM 수신기 |

## <a name="table-4---wap-and-federation-servers"></a>테이블 4 - WAP 및 페더레이션 서버
이 표에서 hello 페더레이션 서버와 WAP 서버 간의 통신에 필요한 hello 포트와 프로토콜을 설명 합니다.

| 프로토콜 | 포트 | 설명 |
| --- | --- | --- |
| HTTPS |443(TCP/UDP) |인증에 사용합니다. |

## <a name="table-5---wap-and-users"></a>테이블 5 - WAP 및 사용자
이 표에서 사용자와 hello WAP 서버 간의 통신에 필요한 hello 포트와 프로토콜을 설명 합니다.

| 프로토콜 | 포트 | 설명 |
| --- | --- | --- |
| HTTPS |443(TCP/UDP) |장치 인증에 사용합니다. |
| TCP |49443(TCP) |인증서 인증에 사용합니다. |

## <a name="table-6a--6b---pass-through-authentication-with-single-sign-on-sso-and-password-hash-sync-with-single-sign-on-sso"></a>테이블 6a / 6b - Single Sign-on(SSO)으로 통과 인증 및 Single Sign-on(SSO)와 암호 해시 동기화
다음 표에서 hello hello Azure AD Connect와 Azure AD 간의 통신에 필요한는 hello 포트와 프로토콜을 설명 합니다.

### <a name="table-6a---pass-through-authentication-with-sso"></a>테이블 6a - SSO로 통과 인증
|프로토콜|포트 번호|설명
| --- | --- | ---
|HTTP|80|SSL과 같은 보안 유효성 검사에 아웃바운드 HTTP 트래픽을 사용하도록 설정합니다. 또한 필요한 hello 커넥터에 대 한 자동 업데이트 기능 toofunction 제대로 합니다.
|HTTPS|443| 활성화 및 비활성화 hello 기능의 커넥터를 등록 하는 중, 커넥터 업데이트를 다운로드 및 모든 사용자 로그인 요청을 처리 등의 작업에 대 한 아웃 바운드 HTTPS 트래픽을 사용 하도록 설정 합니다.

또한 Azure AD Connect 필요한 toobe 수 toomake 직접 IP 연결 toohello [Azure 데이터 센터 IP 범위](https://www.microsoft.com/en-us/download/details.aspx?id=41653)합니다.

### <a name="table-6b---password-hash-sync-with-sso"></a>테이블 6b - SSO와 암호 해시 동기화

|프로토콜|포트 번호|설명
| --- | --- | ---
|HTTPS|443| SSO 등록 (hello SSO 등록 프로세스에만 필요)를 사용 하도록 설정 합니다.

또한 Azure AD Connect 필요한 toobe 수 toomake 직접 IP 연결 toohello [Azure 데이터 센터 IP 범위](https://www.microsoft.com/en-us/download/details.aspx?id=41653)합니다. 이 역시만 hello SSO 등록 프로세스에 필요 합니다.

## <a name="table-7a--7b---azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a>테이블 7a & 7b - (AD FS/동기화)와 Azure AD에 대한 Azure AD Connect Health 에이전트
hello ´ ֲ ַ hello 끝점, 포트 및 Azure AD Connect Health 에이전트와 Azure AD 간의 통신에 필요한 프로토콜

### <a name="table-7a---ports-and-protocols-for-azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a>테이블 7a - Azure AD Connect Health 에이전트(AD FS/동기화)와 Azure AD에 대한 포트 및 프로토콜
이 표에서 아웃 바운드 포트와 프로토콜 hello Azure AD Connect Health 에이전트와 Azure AD 간의 통신에 필요한 다음 hello를 설명 합니다.  

| 프로토콜 | 포트 | 설명 |
| --- | --- | --- |
| HTTPS |443(TCP/UDP) |아웃바운드 |
| Azure Service Bus |5671(TCP/UDP) |아웃바운드 |

### <a name="7b---endpoints-for-azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a>7b - Azure AD Connect Health 에이전트(AD FS/동기화)와 Azure AD에 대한 끝점
끝점의 목록을 참조 하십시오. [hello Azure AD Connect Health agent에 대 한 요구 사항 섹션 hello](../connect-health/active-directory-aadconnect-health-agent-install.md#requirements)합니다.

