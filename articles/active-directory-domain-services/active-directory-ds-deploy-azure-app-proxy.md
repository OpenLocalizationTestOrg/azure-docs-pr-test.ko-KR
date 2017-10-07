---
title: "Azure Active Directory Domain Services: Azure Active Directory 응용 프로그램 프록시 배포 | Microsoft Docs"
description: "Azure Active Directory Domain Services 관리되는 도메인에서 Azure AD 응용 프로그램 프록시 사용"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 4142111231d0256960d0c02d686d51533ba2171c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-ad-application-proxy-on-an-azure-ad-domain-services-managed-domain"></a>Azure AD Domain Services 관리되는 도메인에서 Azure AD 응용 프로그램 프록시 배포
Azure AD (Active Directory) 응용 프로그램 프록시를 사용 하면 온-프레미스 응용 프로그램 toobe hello를 통해 액세스를 게시 하 여 원격 작업자를 지 원하는 인터넷 합니다. Azure AD 도메인 서비스와 온-프레미스 tooAzure 인프라 서비스를 실행 중인 이제 리프트 및-시프트 레거시 응용 프로그램 수 있습니다. 그런 다음 Azure AD 응용 프로그램 프록시, 조직에서 보안 된 원격 액세스 toousers tooprovide hello를 사용 하 여 이러한 응용 프로그램을 게시할 수 있습니다.

새 toohello Azure AD 응용 프로그램 프록시를 사용 하는 경우 자세한 내용은이 기능에 대 한 다음 문서는 hello로: [어떻게 tooprovide 보안 원격 액세스 tooon 온-프레미스 응용 프로그램](../active-directory/active-directory-application-proxy-get-started.md)합니다.


## <a name="before-you-begin"></a>시작하기 전에
이 문서에 나열 된 tooperform hello 작업 해야 합니다.

1. 유효한 **Azure 구독**.
2. **Azure AD 디렉터리** - 온-프레미스 디렉터리 또는 클라우드 전용 디렉터리와 동기화됩니다.
3. **Azure AD Basic 또는 Premium 라이선스** Azure AD 응용 프로그램 프록시 hello toouse 필요 합니다.
4. **Azure AD 도메인 서비스** hello Azure AD 디렉터리를 설정 해야 합니다. 그렇게 하지 않은 경우에 따라 hello에 설명 된 모든 hello 작업 [시작 가이드](active-directory-ds-getting-started.md)합니다.

<br>

## <a name="task-1---enable-azure-ad-application-proxy-for-your-azure-ad-directory"></a>작업 1 - Azure AD Directory에 대한 Azure AD 응용 프로그램 프록시 활성화
Hello 단계 tooenable hello Azure AD 디렉터리에 대 한 Azure AD 응용 프로그램 프록시를 다음을 수행 합니다.

1. Hello에 관리자 권한으로 로그인 [Azure 포털](http://portal.azure.com)합니다.

2. 클릭 **Azure Active Directory** toobring hello directory 개요를 합니다. **엔터프라이즈 응용 프로그램**을 클릭합니다.

    ![Azure AD Directory 선택](./media/app-proxy/app-proxy-enable-start.png)
3. **응용 프로그램 프록시**를 클릭합니다. Azure AD Basic 또는 Azure AD Premium 구독이 없는 경우 옵션 tooenable 평가판을 표시 합니다. 설정/해제 **응용 프로그램 프록시를 사용 하도록 설정?** 너무**사용** 클릭 **저장**합니다.

    ![앱 프록시 사용](./media/app-proxy/app-proxy-enable-proxy-blade.png)
4. toodownload 커넥터 hello, hello 클릭 **커넥터** 단추입니다.

    ![커넥터 다운로드](./media/app-proxy/app-proxy-enabled-download-connector.png)
5. Hello 다운로드 페이지에서 hello 사용 약관 및 개인 정보 보호 계약에 동의 하 고 hello 클릭 **다운로드** 단추입니다.

    ![다운로드 확인](./media/app-proxy/app-proxy-enabled-confirm-download.png)


## <a name="task-2---provision-domain-joined-windows-servers-toodeploy-hello-azure-ad-application-proxy-connector"></a>작업 2-프로 비전 도메인에 가입 된 Windows 서버 toodeploy hello Azure AD 응용 프로그램 프록시 커넥터
Hello Azure AD 응용 프로그램 프록시 커넥터를 설치할 수 있는 도메인에 가입 된 Windows Server 가상 컴퓨터가 있어야 합니다. 게시 되는 hello 응용 프로그램에 따라 tooprovision hello 커넥터가 설치 된 여러 서버를 선택할 수 있습니다. 이 배포 옵션을 선택하면 가용성이 높아지고 더 많은 인증 부하를 처리하는 데 도움이 됩니다.

커넥터 서버 hello를 프로 비전 동일한 가상 네트워크 (또는 연결/겹치기 가상 네트워크)를 사용 하도록 설정한에 hello Azure AD 도메인 서비스 관리 되는 도메인입니다. Hello 응용 프로그램 프록시를 통해 게시 하는 hello 응용 프로그램을 호스트 하는 hello 서버 toobe hello에 설치 해야 하는 마찬가지로 동일한 Azure 가상 네트워크입니다.

tooprovision 커넥터 서버 hello 문서에 설명 된 hello 작업에 따라 [Windows 가상 컴퓨터 tooa 관리 되는 도메인에 가입](active-directory-ds-admin-guide-join-windows-vm.md)합니다.


## <a name="task-3---install-and-register-hello-azure-ad-application-proxy-connector"></a>작업 3-설치 및 등록 hello Azure AD 응용 프로그램 프록시 커넥터
이전에 Windows Server 가상 컴퓨터를 프로 비전 하 고 toohello 관리 되는 도메인 가입 합니다. 이 작업에서는이 가상 컴퓨터에 hello Azure AD 응용 프로그램 프록시 커넥터를 설치 합니다.

1. Hello Azure AD 웹 응용 프로그램 프록시 커넥터를 설치 하는 hello 커넥터 설치 패키지 toohello VM을 복사 합니다.

2. 실행 **AADApplicationProxyConnectorInstaller.exe** hello 가상 컴퓨터에 있습니다. Hello 소프트웨어 사용 조건에 동의 합니다.

    ![설치 조건에 동의](./media/app-proxy/app-proxy-install-connector-terms.png)
3. 설치 하는 동안 Azure AD 디렉터리의 응용 프로그램 프록시 hello로 증명된 tooregister hello 커넥터 됩니다.
    * **Azure AD 전역 관리자 자격 증명**을 제공합니다. 전역 관리자 테넌트는 Microsoft Azure 자격 증명과 다를 수 있습니다.
    * hello 관리자 사용 되는 계정 tooregister hello 커넥터 속해야 toohello hello 응용 프로그램 프록시 서비스를 사용할 수 있는 동일한 디렉터리입니다. 예를 들어 hello 테 넌 트 도메인이 contoso.com 이면 admin 님 안녕하세요 해야 admin@contoso.com 또는 해당 도메인에 있는 다른 모든 유효한 별칭.
    * IE 보안 강화 구성 켜져 hello 서버에 대 한 hello 커넥터 설치 하는 hello 등록 화면이 차단 될 수 있습니다. hello 오류 메시지의 지침에 따라 hello tooallow 액세스 합니다. Internet Explorer 보안 강화가 해제되어 있는지 확인하세요.
    * 커넥터 등록에 실패한 경우 [응용 프로그램 프록시 문제 해결](../active-directory/active-directory-application-proxy-troubleshoot.md)을 참조하세요.

    ![커넥터 설치됨](./media/app-proxy/app-proxy-connector-installed.png)
4. tooensure hello 커넥터 실행된 hello Azure AD 응용 프로그램 프록시 커넥터 문제 해결사는 올바르게 작동 합니다. Hello 문제 해결사를 실행 한 후 성공 보고서에 표시 됩니다.

    ![문제 해결사 성공](./media/app-proxy/app-proxy-connector-troubleshooter.png)
5. Azure AD 디렉터리의 hello 응용 프로그램 프록시 페이지에 나열 된 hello 새로 설치 된 커넥터에 표시 됩니다.

    ![](./media/app-proxy/app-proxy-connector-page.png)

> [!NOTE]
> 여러 서버에서 tooinstall 커넥터 tooguarantee 고가용성 hello Azure AD 응용 프로그램 프록시를 통해 게시 된 응용 프로그램을 인증 하기 위해 선택할 수 있습니다. Hello tooinstall hello 커넥터 다른 서버에 가입된 tooyour 관리 되는 도메인에 위에 나열 된 동일한 단계를 수행 합니다.
>
>

## <a name="next-steps"></a>다음 단계
Hello Azure AD 응용 프로그램 프록시를 설정에 있고 도메인 관리 되는 Azure AD 도메인 서비스와 통합 합니다.

* **응용 프로그램 tooAzure 가상 컴퓨터 마이그레이션:** 리프트 시프트 온-프레미스 서버 tooAzure 가상 컴퓨터에 가입된 tooyour 관리 되는 도메인에서 응용 프로그램 수입니다. 이렇게 하면 서버 온-프레미스를 실행 중인 hello 인프라 비용을 제거 합니다.

* **Azure AD 응용 프로그램 프록시를 사용 하 여 응용 프로그램 게시:** hello Azure AD 응용 프로그램 프록시를 사용 하 여 Azure 가상 컴퓨터에서 실행 되는 응용 프로그램을 게시 합니다. 자세한 내용은 [Azure AD 응용 프로그램 프록시를 사용하여 응용 프로그램 게시](../active-directory/application-proxy-publish-azure-portal.md)를 참조하세요.


## <a name="deployment-note---publish-iwa-integrated-windows-authentication-applications-using-azure-ad-application-proxy"></a>배포 참고 - Azure AD 응용 프로그램 프록시를 사용하여 IWA(Windows 통합 인증) 응용 프로그램 게시
Tooimpersonate 사용자 응용 프로그램 프록시 커넥터 권한을 부여 하 여 통합 IWA (Windows 인증)를 사용 하 여 single sign on tooyour 응용 프로그램을 사용 하도록 설정 하 고 보내고 사용자 대신 토큰을 수신 합니다. 리소스에 대 한 hello 커넥터 toogrant hello 필요한 사용 권한 tooaccess hello 관리 되는 도메인에서 kerberos 제한 위임을 KCD ()를 구성 합니다. 보안 향상된을 위해 관리 되는 도메인에 hello 리소스 기반 KCD 메커니즘을 사용 합니다.


### <a name="enable-resource-based-kerberos-constrained-delegation-for-hello-azure-ad-application-proxy-connector"></a>Hello Azure AD 응용 프로그램 프록시 커넥터에 대 한 리소스 기반 kerberos 제한 위임을 사용 하도록 설정
hello Azure 응용 프로그램 프록시 커넥터에서 구성 해야 (KCD) kerberos 제한 위임에 대 한 사용자를 가장할 수 있으므로 hello 관리 되는 도메인입니다. Azure AD Domain Services 관리되는 도메인에서 도메인 관리자 권한이 없습니다. 따라서 **관리되는 도메인에 기존 계정 수준 KCD를 구성할 수 없습니다**.

이 [문서](active-directory-ds-enable-kcd.md)에 설명된 대로 리소스 기반 KCD를 사용합니다.

> [!NOTE]
> 구성원 toobe 필요한 tooadminister hello hello ' AAD DC Administrators' 그룹의 AD PowerShell cmdlet을 사용 하 여 도메인을 관리 합니다.
>
>

Hello는 hello Azure AD 응용 프로그램 프록시 커넥터가 설치 된 컴퓨터에 대 한 hello Get-adcomputer PowerShell cmdlet tooretrieve hello 설정을 사용 합니다.
```
$ConnectorComputerAccount = Get-ADComputer -Identity contoso100-proxy.contoso100.com
```

그 후 hello Set-adcomputer cmdlet tooset 리소스 기반 KCD 사용 하 여 리소스 서버 hello에 대 한.
```
Set-ADComputer contoso100-resource.contoso100.com -PrincipalsAllowedToDelegateToAccount $ConnectorComputerAccount
```

Tooconfigure 필요한 관리 되는 도메인에서 여러 응용 프로그램 프록시 커넥터를 배포한 경우 이러한 각 커넥터 인스턴스에 대 한 KCD 리소스 기반 합니다.


## <a name="related-content"></a>관련 콘텐츠
* [Azure AD Domain Services - 시작 가이드](active-directory-ds-getting-started.md)
* [관리되는 도메인에서 Kerberos 제한 위임 구성](active-directory-ds-enable-kcd.md)
* [Kerberos 제한 위임 개요](https://technet.microsoft.com/library/jj553400.aspx)
