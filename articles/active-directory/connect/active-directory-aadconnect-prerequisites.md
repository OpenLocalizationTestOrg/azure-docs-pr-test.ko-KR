---
title: "Azure AD Connect: 필수 조건 및 하드웨어 | Microsoft Docs"
description: "이 항목에서는 hello 필수 구성 요소 및 Azure AD Connect에 대 한 hello 하드웨어 요구 사항 설명"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 91b88fda-bca6-49a8-898f-8d906a661f07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2ec8b5da9440c92e8f9d6702d5e5e20de952b588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-for-azure-ad-connect"></a>Azure AD Connect에 대한 필수 조건
이 항목에서는 hello 필수 구성 요소 및 Azure AD Connect에 대 한 hello 하드웨어 요구 사항을 설명 합니다.

## <a name="before-you-install-azure-ad-connect"></a>Azure AD Connect를 설치하기 전에
Azure AD Connect를 설치하기 전에 필요한 몇 가지 사항이 있습니다.

### <a name="azure-ad"></a>Azure AD
* Azure 구독 또는 [Azure 평가판 구독](https://azure.microsoft.com/pricing/free-trial/)입니다. 이 구독에 불과합니다 hello Azure 포털에 액세스 하 고 Azure AD Connect를 사용 하 여에 대 한 하지 필요 합니다. PowerShell 또는 Office 365를 사용 하는 경우 Azure 구독 toouse Azure AD Connect 필요 하지 않는 것입니다. Office 365 라이선스가 있는 경우 hello Office 365 포털을 사용할 수 합니다. 유료 Office 365 라이선스를 가져올 수도 있습니다 hello에 Azure 포털 hello Office 365 포털에서 합니다.
  * Hello를 사용할 수도 있습니다 [Azure 포털](https://portal.azure.com)합니다. 이 포털에는 Azure AD 라이선스가 필요하지 않습니다.
* [추가 도메인 및 확인 hello](../active-directory-domains-add-azure-portal.md) Azure AD에서 toouse를 계획 합니다. 예를 들어 사용자에 대 한 toouse contoso.com을 계획 하 고 있는지 확인 하는 경우이 도메인이 확인 하 고만 hello contoso.onmicrosoft.com 기본 도메인을 사용 하지 않는 합니다.
* Azure AD 테넌트는 기본적으로 5만 개의 개체를 허용합니다. 도메인을 확인 하는 경우 hello 제한은 증가 too300k 개체입니다. Azure AD에 더 많은 개체를 필요한 경우 지원 사례 toohave hello 제한 증가 더욱 해소 tooopen을 할 수 있습니다. 개체가 50만 개 이상 필요한 경우 Office 365, Azure AD Basic, Azure AD Premium 또는 Enterprise Mobility 및 Security와 같은 라이선스가 필요합니다.

### <a name="prepare-your-on-premises-data"></a>온-프레미스 데이터 준비
* 사용 하 여 [idfix 디렉터리](https://support.office.com/article/Install-and-run-the-Office-365-IdFix-tool-f4bd2439-3e41-4169-99f6-3fabdfa326ac) 중복 및 서식 문제가 tooAzure AD 및 Office 365를 동기화 하기 전에 디렉터리에 같은 tooidentify 오류입니다.
* [Azure AD에서 사용하도록 설정할 수 있는 선택적 동기화 기능](active-directory-aadconnectsyncservice-features.md) 을 검토하여 사용하도록 설정해야 할 기능을 평가합니다.

### <a name="on-premises-active-directory"></a>온-프레미스 Active Directory
* hello AD 스키마 버전 및 포리스트 기능 수준이 Windows Server 2003 이상 이어야 합니다. hello 도메인 컨트롤러 hello 스키마 및 포리스트 수준 요구 사항이 충족으로 모든 버전을 실행할 수 있습니다.
* Toouse hello 기능을 계획 하는 경우 **암호 쓰기 저장**, hello 도메인 컨트롤러 (최신 SP)와 Windows Server 2008 이상 이어야 합니다. 또한 DC가 Windows Server 2008(R2 이전 버전)에 있는 경우 [핫픽스 KB2386717](http://support.microsoft.com/kb/2386717)을 적용해야 합니다.
* Azure AD에서 사용 하는 hello 도메인 컨트롤러는 쓰기 가능 해야 합니다. **지원 되지 않습니다** RODC (읽기 전용 도메인 컨트롤러) 및 Azure AD Connect 어긋납니다 어떤 toouse 리디렉션을 작성 합니다.
* **지원 되지 않습니다** toouse 온-프레미스 된 Sld (단일 레이블 도메인)를 사용 하 여 포리스트/도메인입니다.
* **지원 되지 않습니다** toouse 온-프레미스 "점"를 사용 하 여 포리스트/도메인 (이름에 마침표가 ".") NetBios 이름입니다.
* 너무 좋습니다[hello Active Directory 휴지통 사용](active-directory-aadconnectsync-recycle-bin.md)합니다.

### <a name="azure-ad-connect-server"></a>Azure AD Connect 서버
* Azure AD Connect는 Small Business Server 또는 Windows Server Essentials에 설치할 수 없습니다. Windows Server standard 또는 더 나은 hello 서버 사용 해야 합니다.
* hello Azure AD Connect 서버 전체 GUI 설치 되어 있어야 합니다. **지원 되지 않습니다** tooinstall server core에 있습니다.
* Azure AD Connect는 반드시 Windows Server 2008 이상의 버전에 설치되어야 합니다. Express 설정을 사용하는 경우 이 서버는 도메인 컨트롤러 또는 멤버 서버일 수 있습니다. 사용자 지정 설정을 사용 하는 경우 hello 서버 독립 실행형도 수 있으며 toobe 조인된 tooa 도메인이 없습니다.
* Windows Server 2008 또는 Windows Server 2008 r 2에서 Azure AD Connect를 설치 하는 경우 Windows Update에서 있는지 tooapply hello 최신 핫픽스를 확인 합니다. hello 설치가 패치가 적용 되지 않은 서버와 수 toostart 않습니다.
* Toouse hello 기능을 계획 하는 경우 **암호 동기화**, hello Azure AD Connect 서버는 Windows Server 2008 R2 SP1 이상 이어야 합니다.
* Toouse 하려는 경우는 **그룹 관리 서비스 계정은**, hello Azure AD Connect 서버는 Windows Server 2012 이상 이어야 합니다.
* hello Azure AD Connect 서버 있어야 [.NET Framework 4.5.1](#component-prerequisites) 이상 및 [Microsoft PowerShell 3.0](#component-prerequisites) 이상이 설치 되어 있습니다.
* Azure AD Connect 서버 hello에 PowerShell 기록이 그룹 정책을 사용를 사용할 수 없습니다.
* Hello 서버 AD FS 또는 웹 응용 프로그램 프록시 설치 되어 있는 Windows Server 2012 R2 있어야 Active Directory Federation Services를 배포 하는 경우 이후 버전입니다. [Windows 원격 관리](#windows-remote-management) 를 사용할 수 있어야 합니다.
* Active Directory Federation Services를 배포하고 있는 경우 [SSL 인증서](#ssl-certificate-requirements)가 필요합니다.
* Active Directory Federation Services를 배포 하는 경우 tooconfigure 필요한 [이름 확인](#name-resolution-for-federation-servers)합니다.
* 하거나 전역 관리자가 MFA를 사용 하도록 설정 하는 경우 다음 URL hello **https://secure.aadcdn.microsoftonline-p.com** hello 신뢰할 수 있는 사이트 목록에 있어야 합니다. 모르는 증명된 tooadd 하기 전에이 사이트 toohello 신뢰할 수 있는 사이트 목록 MFA 챌린지 및 그에 대 한 메시지가 나타나면 추가 되지 않았습니다. Internet Explorer tooadd를 사용할 수 있습니다이 tooyour 신뢰할 수 있는 사이트입니다.

### <a name="sql-server-used-by-azure-ad-connect"></a>Azure AD Connect에서 사용하는 SQL Server
* Azure AD Connect SQL Server 데이터베이스 toostore id 데이터를 필요합니다. 기본적으로 SQL Server 2012 Express LocalDB(SQL Server Express의 라이트 버전)가 설치됩니다. SQL Server Express에 toomanage 약 100, 000 개체 수 있도록 하는 10GB 크기 제한이 있습니다. 더 많은 양의 디렉터리 개체 toomanage 해야 할 경우 toopoint hello 설치 마법사 tooa 다른 SQL Server 설치를 해야 합니다.
* 별도의 SQL Server를 사용하는 경우 다음 요구 사항이 적용됩니다.
  * Azure AD Connect까지 모든 버전의 SQL Server 2008 (최신 서비스 팩) tooSQL 서버 2016 s p 1에서에서 Microsoft SQL Server를 지원합니다. Microsoft Azure SQL 데이터베이스는 데이터베이스로 **지원되지 않습니다** .
  * 대/소문자를 구분하지 않는 SQL 데이터 정렬을 사용해야 합니다. 이러한 데이터 정렬은 이름에 \_CI_를 사용하여 식별됩니다. **지원 되지 않습니다** 로 식별 되는 대/소문자 구분 데이터 정렬 toouse \_CS_ 이름에 있습니다.
  * SQL 인스턴스당 동기화 엔진을 한 개만 사용할 수 있습니다. **지원 되지 않습니다** tooshare SQL 인스턴스를 FIM/MIM 동기화, DirSync 또는 Azure AD Sync 함께 합니다.

### <a name="accounts"></a>계정
* 원하는와 toointegrate hello Azure AD 테 넌 트에 대 한 Azure AD 전역 관리자 계정. 이 계정은 **학교 또는 조직 계정**이어야 하며 **Microsoft 계정**이 될 수 없습니다.
* Express 설정을 사용하거나 DirSync에서 업그레이드하는 경우 로컬 Active Directory에 대한 엔터프라이즈 관리자 계정이 있어야 합니다.
* [Active Directory의 계정](active-directory-aadconnect-accounts-permissions.md) hello 설정 사용자 지정 설치 경로 사용 하는 경우.

### <a name="connectivity"></a>연결
* hello Azure AD Connect 서버 인트라넷 및 인터넷 모두에 대 한 DNS 확인을 해야합니다. hello DNS 서버 있어야 tooresolve 이름을 tooyour 온-프레미스 Active Directory 및 hello Azure AD 끝점입니다.
* 인트라넷에서 방화벽을 설정한 hello Azure AD Connect 서버와 도메인 컨트롤러 간의 tooopen 포트를 필요로 하는 경우 다음 참조 [Azure AD Connect 포트](active-directory-aadconnect-ports.md) 자세한 정보에 대 한 합니다.
* Url에 액세스할 수 있는 프록시 또는 방화벽 제한에는 다음 Url에 문서화 되어 hello 경우 [Office 365 Url 및 IP 주소 범위](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) 열려 있어야 합니다.
  * 사용 하는 경우 Microsoft 클라우드 독일 또는 Microsoft Azure Government 클라우드 hello hello 다음 참조 [Azure AD Connect 동기화 서비스 인스턴스 고려 사항](active-directory-aadconnect-instances.md) Url에 대 한 합니다.
* Azure AD Connect toocommunicate TLS 1.0을 사용 하 여 Azure AD와 기본적으로는 것입니다. Hello 단계를 수행 하 여이 tooTLS 1.2를 변경할 수 있습니다 [Azure AD Connect에 대 한 TLS 1.2를 사용 하도록 설정](#enable-tls-12-for-azure-ad-connect)합니다.
* 아웃 바운드 프록시 toohello 인터넷에 연결 하기 위한를 사용 하는 경우 hello hello 설정을 다음 **C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config** hello 설치 마법사에 대 한 파일을 추가 해야 합니다 Azure AD Connect 동기화 toobe 수 tooconnect toohello 인터넷 및 Azure AD. 이 텍스트는 hello hello 파일 맨 아래에 입력 해야 합니다. 이 코드에서는 &lt;PROXYADRESS&gt; 나타냅니다 hello 실제 프록시 IP 주소 또는 호스트 이름입니다.

```
    <system.net>
        <defaultProxy>
            <proxy
            usesystemdefault="true"
            proxyaddress="http://<PROXYADDRESS>:<PROXYPORT>"
            bypassonlocal="true"
            />
        </defaultProxy>
    </system.net>
```

* 프록시 서버에 필요한 인증을 다음 hello 경우 [서비스 계정](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) 있어야 hello에 도메인을 사용 해야 사용자 지정 하는 hello 설정을 설치 경로 toospecify는 [사용자 지정 서비스 계정](active-directory-aadconnect-get-started-custom.md#install-required-components). 서로 다른 변경 toomachine.config을 해야합니다. Machine.config의이 변경으로 hello 설치 마법사 및 동기화 엔진 hello 프록시 서버에서 tooauthentication 요청에 응답 합니다. Hello를 제외한 모든 설치 마법사 페이지에서 **구성** 페이지 hello 사용자의 로그인 자격 증명이 사용 됩니다. Hello에 **구성** hello 설치 마법사, hello 컨텍스트 hello 끝에서 페이지는 스위치가 toohello [서비스 계정](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) 에 사용자에 의해 만들어진 합니다. hello machine.config 섹션은 다음과 같이 표시 됩니다.

```
    <system.net>
        <defaultProxy enabled="true" useDefaultCredentials="true">
            <proxy
            usesystemdefault="true"
            proxyaddress="http://<PROXYADDRESS>:<PROXYPORT>"
            bypassonlocal="true"
            />
        </defaultProxy>
    </system.net>
```

* Azure AD Connect 디렉터리 동기화의 일부로 AD는 웹 요청 tooAzure 보내면 Azure AD too5 분 toorespond 차지할 수 있습니다. 일반적으로 프록시 서버 toohave 연결 유휴 시간 제한 구성 됩니다. Hello 구성은 최소 6 분 이상 tooat 설정 확인 하십시오.

자세한 내용은 hello에 대 한 MSDN 참조 [기본 프록시 요소](https://msdn.microsoft.com/library/kd3cf2ex.aspx)합니다.  
연결에 문제가 있는 경우 [연결 문제 해결](active-directory-aadconnect-troubleshoot-connectivity.md)을 참조하세요.

### <a name="other"></a>기타
* 선택 사항: 테스트 사용자 계정 tooverify 동기화 합니다.

## <a name="component-prerequisites"></a>구성 요소 필수 조건
### <a name="powershell-and-net-framework"></a>PowerShell 및 .Net Framework
Azure AD Connect는 Microsoft PowerShell 및 .NET Framework 4.5.1에 따라 다릅니다. 서버에 이 버전 이상을 설치해야 합니다. Windows Server 버전에 따라 수행 hello를 수행 합니다.

* Windows Server 2012R2
  * Microsoft PowerShell은 기본적으로 설치되므로 별도의 작업이 필요하지 않습니다.
  * .NET Framework 4.5.1 이후 릴리스는 Windows 업데이트를 통해 제공됩니다. Hello 제어판에서에서 hello 최신 업데이트 tooWindows 서버를 설치 했는지 확인 합니다.
* Windows Server 2008R2 및 Windows Server 2012
  * hello 최신 버전의 Microsoft PowerShell은 영어로 **Windows Management Framework 4.0**다운로드 가능 [Microsoft 다운로드 센터](http://www.microsoft.com/downloads)합니다.
  * .NET Framework 4.5.1과 이후 릴리스는 [Microsoft 다운로드 센터](http://www.microsoft.com/downloads)에서 찾을 수 있습니다.
* Windows Server 2008
  * hello 지 원하는 최신 버전의 PowerShell은 영어로 **Windows Management Framework 3.0**다운로드 가능 [Microsoft 다운로드 센터](http://www.microsoft.com/downloads)합니다.
  * .NET Framework 4.5.1과 이후 릴리스는 [Microsoft 다운로드 센터](http://www.microsoft.com/downloads)에서 찾을 수 있습니다.

### <a name="enable-tls-12-for-azure-ad-connect"></a>Azure AD Connect에 TLS 1.2 사용
Azure AD Connect는 hello 동기화 엔진 서버와 Azure AD 간의 hello 통신을 암호화 하기 위해 기본적으로 TLS 1.0를 사용 합니다. Hello 서버에서 기본적으로.Net 응용 프로그램 toouse TLS 1.2를 구성 하 여이 변경할 수 있습니다. TLS 1.2에 대한 자세한 내용은 [Microsoft 보안 권고 2960358](https://technet.microsoft.com/security/advisory/2960358)에서 찾을 수 있습니다.

1. Windows Server 2008에서는 TLS 1.2를 사용할 수 없습니다. Windows Server 2008R2 이상이 필요합니다. 참조 하십시오 hello.Net 4.5.1 핫픽스를 운영 체제에 설치 하면 [Microsoft 보안 권고 2960358](https://technet.microsoft.com/security/advisory/2960358)합니다. 이 핫픽스 또는 이후 릴리스를 서버에 이미 설치했을 수 있습니다.
2. Windows Server 2008R2를 사용하는 경우 TLS 1.2가 사용되도록 설정되어 있는지 확인합니다. Windows Server 2012 서버 및 이후 버전에서는 TLS 1.2가 이미 사용되도록 설정되어 있습니다.
   ```
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2]
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client] "DisabledByDefault"=dword:00000000 "Enabled"=dword:00000001
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server] "DisabledByDefault"=dword:00000000 "Enabled"=dword:00000001
   ```
3. 모든 운영 체제에 대 한이 레지스트리 키를 설정 하 고 hello 서버를 다시 시작 합니다.
   ```
   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319
   "SchUseStrongCrypto"=dword:00000001
   ```
4. 또한 hello 동기화 엔진 서버와 원격 SQL Server, TLS 1.2 tooenable 합니다 필요한 hello 버전에 대 한 설치 되어 있는 있는지 확인 하십시오 [Microsoft SQL Server에 대 한 TLS 1.2 지원](https://support.microsoft.com/kb/3135244)합니다.

## <a name="prerequisites-for-federation-installation-and-configuration"></a>페더레이션 설치 및 구성을 위한 필수 조건
### <a name="windows-remote-management"></a>Windows 원격 관리
Azure AD Connect toodeploy Active Directory Federation Services 또는 hello 웹 응용 프로그램 프록시를 사용 하면 이러한 요구 사항 확인:

* Hello 대상 서버가 도메인에 가입 된 경우의 Windows 원격 관리 설정 되어 있는지 확인 한 다음
  * 관리자 권한 PSH 명령 창에서 `Enable-PSRemoting –force`
* 도메인이 아닌 WAP 컴퓨터를 가입 hello 대상 서버를 사용 하는 경우 다음는 몇 가지 추가 요구 사항
  * Hello 대상 컴퓨터 (WAP 컴퓨터):
    * 확인 hello winrm (Windows 원격 관리 / WS 관리) hello 서비스 스냅인을 통해 서비스가 실행 되 고
    * 관리자 권한 PSH 명령 창에서 `Enable-PSRemoting –force`
  * Hello 컴퓨터는 hello에 마법사가 실행 중 (hello 대상 컴퓨터가 도메인에 가입 되어 있거나 신뢰할 수 없는 도메인 경우):
    * 고급 PSH 명령 창에서 hello 명령을 사용 하 여`Set-Item WSMan:\localhost\Client\TrustedHosts –Value <DMZServerFQDN> -Force –Concatenate`
    * 서버 관리자:
      * DMZ WAP 호스트 toomachine 풀 추가 (서버 관리자-> 관리-> 서버 추가... S 탭 사용)
      * 서버 관리자 모두 서버 탭: WAP 서버를 마우스 오른쪽 단추로 클릭 하 고 관리 이름으로 저장...를 선택, hello WAP 컴퓨터에 대 한 로컬 (도메인) 자격 증명을 입력 합니다.
      * toovalidate 원격 PSH 연결을 hello 서버 관리자 모두 서버 탭에서: WAP 서버를 마우스 오른쪽 단추로 클릭 하 고 Windows PowerShell을 선택 합니다. 원격 PSH 세션을 열어야 하는지를 tooensure 원격 PowerShell 세션을 설정할 수 있습니다.

### <a name="ssl-certificate-requirements"></a>SSL 인증서 요구 사항
* 이 가장 좋습니다 toouse AD FS 팜의 모든 노드 및 모든 웹 응용 프로그램 프록시 서버에서 같은 SSL 인증서를 hello 합니다.
* hello 인증서는 X509 해야 인증서입니다.
* 테스트 랩 환경의 페더레이션 서버에서 자체 서명된 인증서를 사용할 수 있습니다. 그러나 프로덕션 환경에 대 한 공용 CA에서 hello 인증서를 가져와야 하는 것이 좋습니다.
  * 각 웹 응용 프로그램 프록시 서버에 설치 하는 hello 인증서가 두 hello 로컬 서버와 모든 페더레이션 서버에 신뢰할 수 있는 공개적으로 신뢰할 수 없는 인증서를 사용 하는 경우 확인
* hello 인증서 hello id hello 페더레이션 서비스 이름 (예: sts.contoso.com) 일치 해야 합니다.
  * hello id는 dNSName 종류의 중 하나는 주체 대체 이름 (SAN) 확장 또는 hello 주체 이름으로 지정 SAN 항목이 없는 경우 일반 이름입니다.  
  * 여러 SAN 항목 hello 페더레이션 서비스 이름과 일치 그 중 하나가 제공 hello 인증서에 있을 수 있습니다.
  * 작업 공간 연결 toouse를 계획 하는 경우 추가 SAN hello 값 입력 해야 합니다. **enterpriseregistration 합니다.** 조직의 예를 들어 hello 주 UPN (사용자 이름) 접미사 뒤 **enterpriseregistration.contoso.com**합니다.
* CryptoAPI 다음 세대(CNG) 및 키 저장소 공급자를 기반으로 하는 인증서는 지원되지 않습니다. 즉, KSP(키 저장소 공급자)가 아닌 CSP(암호화 서비스 공급자)를 기반으로 인증서를 사용해야 합니다.
* 와일드카드 인증서가 지원됩니다.

### <a name="name-resolution-for-federation-servers"></a>페더레이션 서버에 대한 이름 확인
* (내부 DNS 서버) hello 인트라넷 및 엑스트라넷 hello (공용 DNS 도메인 등록자를 통해)에 대 한 AD FS 페더레이션 서비스 이름 (예: sts.contoso.com) hello에 대 한 DNS 레코드를 설정 합니다. Hello 인트라넷 DNS 레코드를 위해 다음과 같이 A를 사용 하는 레코드 및 CNAME 레코드를 제외 합니다. 이 명령은 도메인에 가입 된 컴퓨터에서 제대로 windows 인증 toowork에 필요 합니다.
* 둘 이상의 AD FS 서버 또는 웹 응용 프로그램 프록시 서버를 배포 하는 경우에 hello AD FS 페더레이션 서비스 이름 (예: sts.contoso.com) 지점 toohello에 대 한 DNS 레코드 hello 부하 분산 장치 및 부하 분산 장치를 구성 했는지 확인 합니다.
* 인트라넷에서 Internet Explorer를 사용 하 여 브라우저 응용 프로그램에 대 한 windows 통합된 인증 toowork에 대 한 해당 hello AD FS 페더레이션 서비스 이름 (예: sts.contoso.com)가 IE에서 toohello 인트라넷 영역을 추가 확인 합니다. 이 제어 배포 tooall 및 그룹 정책을 통해 도메인 연결 컴퓨터입니다.

## <a name="azure-ad-connect-supporting-components"></a>Azure AD Connect 지원 구성 요소
hello 다음은 Azure AD Connect가 설치 되어 있는 hello 서버에 Azure AD Connect를 설치 하는 구성 요소의 목록입니다. 이 목록은 기본 Express 설치에 해당합니다. Toouse 다른 SQL Server를 선택할 경우 hello에 동기화 서비스 페이지를 설치, 다음 SQL Express LocalDB 설치 되어 있지 않습니다 로컬로 합니다.

* Azure AD Connect Health
* IT 전문가를 위한 Microsoft Online Services 로그인 도우미(설치되지만 종속되지 않음)
* Microsoft SQL Server 2012 명령줄 유틸리티
* Microsoft SQL Server 2012 Express LocalDB
* Microsoft SQL Server 2012 Native Client
* Microsoft Visual C++ 2013 재배포 패키지

## <a name="hardware-requirements-for-azure-ad-connect"></a>Azure AD Connect의 하드웨어 요구 사항
hello 표에서 hello hello Azure AD Connect 동기화 컴퓨터에 대 한 최소 요구 사항을 보여 줍니다.

| Active Directory의 개체 수 | CPU | 메모리 | 하드 드라이브 크기 |
| --- | --- | --- | --- |
| 10,000개 미만 |1.6GHz |4GB |70GB |
| 10,000–50,000개 |1.6GHz |4GB |70GB |
| 50,000–100,000개 |1.6GHz |16GB |100GB |
| 100, 000 개 이상의 개체에 대 한 hello 정식 버전의 SQL Server가 필요 | | | |
| 100,000–300,000개 |1.6GHz |32GB |300GB |
| 300,000–600,000개 |1.6GHz |32GB |450GB |
| 600,000개 초과 |1.6GHz |32GB |500GB |

AD FS를 실행 하는 컴퓨터에 대 한 최소 요구 사항을 hello 또는 웹 응용 프로그램 서버 hello 다음:

* CPU: 듀얼 코어 1.6GHz 이상
* 메모리: 2GB 이상
* Azure VM: A2 구성 이상

## <a name="next-steps"></a>다음 단계
[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.
