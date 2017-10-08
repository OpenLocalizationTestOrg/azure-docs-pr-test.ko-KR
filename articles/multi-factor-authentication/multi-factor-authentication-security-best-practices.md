---
title: "MFA에 대 한 유용한 aaaSecurity | Microsoft Docs"
description: "이 문서에서는 Azure 계정으로 Azure MFA를 사용하는 모범 사례를 제공합니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3be7d968-96bb-4320-8701-869fd04a2595
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 7f18c2592764878b842d81783b321a05f29ee3d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security-best-practices-for-using-azure-multi-factor-authentication-with-azure-ad-accounts"></a>Azure AD 계정으로 Azure Multi-Factor Authentication을 사용하기 위한 보안 모범 사례

2 단계 인증은 원하는 tooenhance의 인증 프로세스는 대부분의 조직은 hello 기본 선택입니다. Azure MFA(Multi-Factor Authentication)를 사용하면 회사에서 자체의 보안 및 준수 요구사항을 충족하면서도 사용자에게 단순한 로그인 경험을 제공할 수 있습니다. 이 문서에서는 Azure MFA hello 채택을 계획할 때 고려해 야 할 몇 가지 팁을 설명 합니다.

## <a name="deploy-azure-mfa-in-hello-cloud"></a>Hello 클라우드에서 Azure MFA를 배포 합니다.

모든 사용자를 위한 두 가지 방법으로 tooenable Azure MFA 가지가 있습니다.

* 각 사용자에 대해 라이선스 구입(Azure MFA, Azure AD Premium 또는 Enterprise Mobility + Security)
* Multi-Factor Auth 공급자 및 사용자 기준 또는 인증 기준 요금제 만들기

### <a name="licenses"></a>라이선스
![EMS](./media/multi-factor-authentication-security-best-practices/ems.png)

Azure AD Premium 또는 Enterprise Mobility + Security 라이선스가 있는 경우 Azure MFA가 이미 있는 것입니다. 조직에 모두 추가 tooextend hello 2 단계 확인 기능 tooall 사용자가 필요 하지 않습니다. Tooassign 라이선스 tooa 사용자 하기만 하 고 MFA를 켤 수 있습니다.

Multi-factor Authentication을 설정할 때 다음 팁 hello를 고려 합니다.

* 인증 기준 Multi-Factor Auth 공급자를 만들지 않도록 합니다. 이렇게 하면 이미 라이선스가 있는 사용자로부터 지불 확인 요청이 발생할 수 있습니다.
* 모든 사용자를 위한 충분 한 라이선스 없다면 조직의 사용자 단위 Multi-factor Auth 공급자 toocover hello rest를 만들 수 있습니다. 
* Azure AD Connect는 온-프레미스 Active Directory 환경을 Azure AD 디렉터리와 동기화하는 경우에만 필요합니다. Active Directory의 온-프레미스 인스턴스와 동기화되지 않은 Azure AD 디렉터리를 사용하는 경우에는 Azure AD Connect가 필요하지 않습니다.

### <a name="multi-factor-auth-provider"></a>Multi-Factor Auth 공급자
![Multi-Factor Auth 공급자](./media/multi-factor-authentication-security-best-practices/authprovider.png)

Azure MFA를 포함하는 라이선스가 없는 경우 MFA Auth 공급자를 만들 수 있습니다. 

Hello 인증 공급자를 만들 때 디렉터리 tooselect 필요 하 고 hello 다음 세부 정보를 고려 합니다.

* Azure AD 디렉터리 toocreate Multi-factor Auth 공급자 필요는 없지만 하나 더 많은 기능을 활용 합니다. 같은 기능 hello은 Azure AD 디렉터리 hello 인증 공급자에 연결할 때 사용 됩니다.  
  * 2 단계 확인 tooall 사용자에 게 확장  
  * 전역 관리자에 게 문의 hello 관리 포털, 사용자 지정 인사말, 보고서 등의 추가 기능을 제공 합니다.
* 온-프레미스 Active Directory 환경을 Azure AD 디렉터리와 동기화하는 경우 DirSync 또는 AAD Sync가 필요합니다. Active Directory의 온-프레미스 인스턴스와 동기화되지 않은 Azure AD 디렉터리를 사용하는 경우에는 DirSync 또는 AAD 동기화가 필요하지 않습니다.
* 비즈니스에 가장 적합 한 hello 소비 모델을 선택 합니다. Hello 사용 모델을 선택한 후에 변경할 수 없습니다. hello 두 개의 모델은 같습니다.
  * 인증 기준: 각 인증에 대한 요금을 청구합니다. 특정 사용자가 아닌 특정 앱에 액세스하는 사용자에 대한 2단계 인증을 하려는 경우 이 모델을 사용합니다.
  * 활성화된 사용자 당: Azure MFA에 대해 사용하도록 설정한 각 사용자에 대한 요금을 청구합니다. 일부 사용자가 Azure AD Premium 또는 Enterprise Mobility Suite 라이선스를 갖고 일부 사용자가 라이선스를 갖지 않은 경우 이 모델을 사용합니다.

### <a name="supportability"></a>지원 가능성
대부분의 사용자가 익숙한 toousing 암호만 tooauthenticate 경우에 회사 제공 tooall 사용자가이 프로세스에 대 한 인식 하는 것이 중요 합니다. 이 인식 관련된 tooMFA 사소한 문제에 대 한 지원 센터를 호출할 사용자 hello 가능성을 줄일 수 있습니다. 그러나 MFA를 일시적으로 비활성화가 필요한 시나리오도 있습니다. 방법 지침 toounderstand 다음 사용 하 여 hello toohandle 그러한 시나리오:

* 기술 지원 담당자 toohandle 시나리오를 hello 사용자 로그인 할 수 없습니다 hello 모바일 앱 또는 전화를 받지 알림 또는 전화 통화를 학습 합니다. 기술 지원 수 [일회성 바이패스를 사용 하도록 설정](multi-factor-authentication-whats-next.md#one-time-bypass) tooallow 사용자 tooauthenticate "무시" 2 단계 인증 하 여 한 번입니다. hello 바이패스는 일시적 이며 지정된 된 수의 시간 (초) 후에 만료 됩니다.
* Hello 고려 [신뢰할 수 있는 Ip 기능](multi-factor-authentication-whats-next.md#trusted-ips) 방식으로 toominimize 2 단계 인증으로 Azure MFA에 있습니다. 이 기능을 관리 되는 또는 페더레이션된 테 넌 트의 관리자가 사용자 hello 회사의 로컬 인트라넷에서 로그인에 대 한 2 단계 인증을 무시할 수 있습니다. hello 기능은 Azure AD Premium, Enterprise Mobility Suite 또는 Azure Multi-factor Authentication 라이선스가 있는 Azure AD 테 넌 트에 사용할 수 있습니다.

## <a name="best-practices-for-an-on-premises-deployment"></a>온-프레미스 배포에 대한 모범 사례
회사를 결정 tooleverage 자체 인프라 tooenable MFA, Azure Multi-factor Authentication 서버 온-프레미스 toodeploy를 할 수 있습니다. hello MFA 서버 구성 요소는 hello 다음 다이어그램에에서 나와 있습니다.

![기본 MFA 서버 구성 요소: 콘솔, 동기화 엔진, 관리 포털, 클라우드 서비스](./media/multi-factor-authentication-security-best-practices/server.png) \*기본적으로 설치되지 않음\** 설치되지만 기본적으로 사용되지 않도록 설정됨

Azure Multi-Factor Authentication Server는 페더레이션을 사용하여 클라우드 리소스 및 온-프레미스 리소스의 보안을 유지할 수 있습니다. AD FS를 보유하고 이를 Azure AD 테넌트와 페더레이션해야 합니다.
Multi-factor Authentication 서버를 설정할 때는 hello 다음 세부 정보를 고려 합니다.

* Hello 첫 번째 확인 단계를 수행 하는 다음에 Active Directory Federation Services (AD FS)를 사용 하 여 Azure AD 리소스를 보호 하 고 있을 경우 온-프레미스 AD FS를 사용 하 여 합니다. hello 두 번째 단계는 hello 클레임을 적용 하 여 수행된 된 온-프레미스를입니다.
* Azure Multi-factor Authentication 서버 AD FS 페더레이션 서버 tooinstall hello가 필요는 없습니다. 그러나 AD FS를 실행 하는 Windows Server 2012 R2에 hello AD FS에 대 한 Multi-factor Authentication 어댑터를 설치 해야 합니다. 것이 지원 되는 버전으로 hello 서버를 다른 컴퓨터에 설치 하 고 AD FS 페더레이션 서버에서 개별적으로 hello AD FS 어댑터를 설치할 수 있습니다. 
* hello Multi-factor Authentication AD FS 어댑터 설치 마법사 Active Directory에서 PhoneFactor Admins 라는 보안 그룹을 만들고 AD FS 서비스 계정 toothis 그룹을 추가 합니다. 도메인 컨트롤러에서 생성 된 hello PhoneFactor Admins 그룹 및 그 hello AD FS 서비스 계정을이 그룹의 구성원임을 확인 합니다. 필요한 경우 hello AD FS 서비스 계정을 PhoneFactor Admins 그룹 toohello를 수동으로 도메인 컨트롤러에 추가 합니다.

### <a name="user-portal"></a>사용자 포털
hello 사용자 포털 셀프 서비스 기능을 허용 하 고 사용자 관리 기능의 전체 집합을 제공 합니다. IIS(인터넷 정보 서버) 웹 사이트에서 실행됩니다. 다음 지침 tooconfigure hello이 구성이 요소를 사용 합니다.

* IIS 6 이상 사용
* ASP.NET v2.0.507207 설치 및 등록
* 이 서버를 경계 네트워크에 배포할 수 있는지 확인합니다.

### <a name="app-passwords"></a>앱 암호
Azure AD와 SSO에 대 한 페더레이션 조직의 toobe Azure MFA를 사용 하는 것을 다음 다음 세부 정보는 hello 고려해 야 합니다.

* hello 응용 프로그램 암호는 Azure AD에서 확인 하 고 따라서 페더레이션을 바이패스 합니다. 앱 암호를 설정할 때에만 페더레이션이 사용됩니다.
* 페더레이션된 (SSO) 사용자에 대 한 암호는 hello 조직 id에 저장 됩니다. Hello 사용자가 회사 hello를 완료 하는 경우 해당 정보에 DirSync를 사용 하 여 tooflow tooorganizational id입니다. 계정 비활성화/삭제는 Azure AD에서 앱 암호 사용 안 함/삭제가 지연 toothree 시간 toosync를 차지할 수 있습니다.
* 앱 암호를 사용할 경우 온-프레미스 클라이언트 액세스 제어 설정은 적용되지 않습니다.
* 온-프레미스 인증 로깅/감사 기능은 앱 암호에 사용할 수 없습니다
* 특정 고급 아키텍처 디자인은 클라이언트와 2단계 인증을 사용하는 경우 인증 위치에 따라 조직의 사용자 이름과 암호 및 앱 암호를 조합하여 사용할 필요가 있습니다. 온-프레미스 인프라에 대해 인증하는 클라이언트의 경우 조직의 사용자 이름과 암호를 사용합니다. Azure AD에 대해 인증 하는 클라이언트 hello 앱 암호를 사용 합니다.
* 기본적으로 사용자가 앱 암호를 만들 수 없습니다. Tooallow 사용자 toocreate 앱 암호가 필요한 경우 선택 hello **비 브라우저 응용 프로그램에 사용자가 toocreate 앱 암호 toosign 허용** 옵션입니다.

## <a name="additional-considerations"></a>추가 고려 사항
온-프레미스로 배포할 각 구성 요소에 대한 추가 고려 사항 및 지침을 보려면 다음 목록을 사용하세요.

- [Active Directory Federation Service](multi-factor-authentication-get-started-adfs.md)를 사용하여 Azure Multi-Factor Authentication 설정
- 설정 및 구성 된 Azure MFA 서버 hello [RADIUS 인증](multi-factor-authentication-get-started-server-radius.md)합니다.
- 설정 및 구성 된 Azure MFA 서버 hello [IIS 인증](multi-factor-authentication-get-started-server-iis.md)합니다.
- 설정 및 구성 된 Azure MFA 서버 hello [Windows 인증](multi-factor-authentication-get-started-server-windows.md)합니다.
- 설정 및 구성 된 Azure MFA 서버 hello [LDAP 인증](multi-factor-authentication-get-started-server-ldap.md)합니다.
- 설정 및 구성 Azure MFA 서버 함께 사용 hello [원격 데스크톱 게이트웨이 및 Azure Multi-factor Authentication 서버 RADIUS를 사용 하 여](multi-factor-authentication-get-started-server-rdg.md)합니다.
- 설정 하 고 hello Azure MFA 서버 간의 동기화를 구성 하 고 [Windows Server Active Directory](multi-factor-authentication-get-started-server-dirint.md)합니다.
- [Hello Azure Multi-factor Authentication 서버 모바일 앱 웹 서비스를 배포](multi-factor-authentication-get-started-server-webservice.md)합니다.
- LDAP 또는 RADIUS를 사용하여 Cisco ASA, Citrix Netscaler 및 Juniper/Pulse Secure VPN 어플라이언스에 대해 [Azure Multi-Factor Authentication을 통한 고급 VPN 구성](multi-factor-authentication-advanced-vpn-configurations.md)

## <a name="next-steps"></a>다음 단계
이 문서에서는 Azure MFA에 대한 몇 가지 모범 사례를 강조하지만 MFA 배포를 계획하는 동안에도 사용할 수 있는 다른 리소스가 있습니다. hello 목록 아래에이 과정에서 활용할 수 있는 몇 가지 주요 문서에 있습니다.

* [Azure Multi-Factor Authentication에서 보고서](multi-factor-authentication-manage-reports.md)
* [hello 2 단계 확인 등록 경험](multi-factor-authentication-end-user-first-time.md)
* [Azure Multi-Factor Authentication FAQ](multi-factor-authentication-faq.md)

