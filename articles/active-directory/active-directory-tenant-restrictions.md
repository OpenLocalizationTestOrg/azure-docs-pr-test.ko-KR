---
title: "테 넌 트-Azure 제한 하 여 aaaManage 액세스 toocloud 앱 | Microsoft Docs"
description: "앱에 액세스할 수 있는 사용자 toouse 테 넌 트 제한 toomanage 자신의 Azure AD 테 넌 트에 따라 방법"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: kgremban
ms.openlocfilehash: 6470fa217738b29104353ae17a2f53216f825c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-tenant-restrictions-toomanage-access-toosaas-cloud-applications"></a>테 넌 트 제한 toomanage 액세스 tooSaaS 클라우드 응용 프로그램을 사용 하 여

보안을 강조 하는 대규모 조직의 Office 365와 같은 toomove toocloud 서비스 하지만 필요성 tooknow 사용자만 액세스할 수 있는 리소스를 승인 합니다. 일반적으로 회사 제한 된 도메인 이름 또는 IP 주소 toomanage 액세스 하려는 경우. 이 방법은 SaaS 앱이 공용 클라우드에서 호스트되고 outlook.office.com 및 login.microsoftonline.com와 같은 공유 도메인 이름으로 실행되는 환경에서는 실패합니다. 이러한 주소를 차단 하면 단순히 tooapproved id 및 리소스 제한 하는 대신 hello 웹에서 Outlook을 완전히에 액세스할 사용자가 지속적 합니다.

Azure Active Directory 솔루션 toothis 챌린지는 테 넌 트 제한 하는 기능입니다. 테 넌 트 제한을 사용 하면 조직 toocontrol 액세스 tooSaaS 클라우드 single sign on에 대 한 hello Azure AD 테 넌 트 hello 응용 프로그램 사용에 따라 응용 프로그램입니다. 예를 들어 tooallow 액세스 tooyour 조직 Office 365 응용 프로그램의 경우 이러한 동일한 응용 프로그램의 액세스 tooother 조직의 인스턴스 방지 하는 동안 좋습니다.  

테 넌 트 제한에는 사용자에 게는 tooaccess를 허용 하는 테 넌 트의 조직 hello 기능 toospecify hello 목록을 제공 합니다. 그런 다음 azure AD 액세스 허용 toothese 테 넌 트 부여합니다.

Office 365에 대 한이 문서에서는 테 넌 트 제한 되지만 hello 기능 해야 Azure ad single sign-on에 대 한 최신 인증 프로토콜을 사용 하는 SaaS 클라우드 앱을 사용할 수 있습니다. 다른 Azure AD 사용 하 여 앱 Office 365에서 사용 하는 hello 테 넌 트의 테 넌 트 SaaS를 사용 하는 경우 필요한 모든 테 넌 트 허용 해야 합니다. SaaS 클라우드 앱에 대 한 자세한 내용은 참조 hello [Active Directory Marketplace](https://azure.microsoft.com/en-us/marketplace/active-directory/)합니다.

## <a name="how-it-works"></a>작동 방법

hello 전체 솔루션 가이드 다음과 같은 구성 요소가 hello: 

1. **Azure AD** – 경우 hello `Restrict-Access-To-Tenants: <permitted tenant list>` 는, Azure AD hello에 대 한 보안 토큰 문제 테 넌 트를 허용 합니다. 

2. **온-프레미스 프록시 서버 인프라** – SSL 검사를 hello 목록을 포함 하는 구성 된 tooinsert hello 헤더 수 있는 프록시 장치에 Azure AD에 대 한 트래픽이 테 넌 트를 허용 합니다. 

3. **클라이언트 소프트웨어** – toosupport 테 넌 트 제한 사항, 클라이언트 소프트웨어 요청 해야 토큰 Azure AD에서 직접 hello 프록시 인프라에서 트래픽을 가로챌 수 있도록 합니다. 최신 인증(예: OAuth 2.0)이 사용될 경우 브라우저 기반 Office 365 응용 프로그램 및 Office 클라이언트에서 테넌트 제한을 지원합니다. 

4. **최신 인증** – 클라우드 서비스에는 최신 인증 toouse 테 넌 트 제한 사용 해야 하 고 블록 tooall 허용 아닌 테 넌 트에 액세스 합니다. Office 365 클라우드 서비스는 기본적으로 구성 된 toouse 최신 인증 프로토콜 이어야 합니다. Hello 최신 인증에 대 한 Office 365 지원에 대 한 최신 정보를 읽을 [업데이트 Office 365 최신 인증](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/)합니다.

다음 다이어그램 hello hello 높은 수준의 트래픽 흐름을 보여 줍니다. SSL 검사 트래픽 tooAzure AD Office 365 클라우드 서비스가 아닌 toohello에만 필요 합니다. 인증 tooAzure AD에 대 한 hello 트래픽 볼륨은 일반적으로 Exchange Online 및 SharePoint Online와 같은 트래픽 볼륨 tooSaaS 응용 프로그램 보다 훨씬 짧기 때문에 이러한 구분은 중요 합니다.

![테넌트 제한 트래픽 흐름 - 다이어그램](./media/active-directory-tenant-restrictions/traffic-flow.png)

## <a name="set-up-tenant-restrictions"></a>테넌트 제한 설정

테 넌 트 제한으로 시작 하는 두 단계 tooget 가지가 있습니다. hello 첫 번째 단계는 클라이언트 toohello 오른쪽 주소에 연결할 수 있는지 toomake입니다. hello 둘째 tooconfigure을 프록시 인프라는 합니다.

### <a name="urls-and-ip-addresses"></a>URL 및 IP 주소

테 넌 트 제한 toouse 클라이언트 수 tooconnect toohello 다음 Azure AD Url tooauthenticate 여야 합니다: login.microsoftonline.com, login.microsoft.com, 및 login.windows.net 합니다. Office 365 tooaccess 클라이언트 수 tooconnect toohello Fqdn/Url 수도 있어야 하 고 IP 주소에 정의 된 또한 [Office 365 Url 및 IP 주소 범위](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)합니다. 

### <a name="proxy-configuration-and-requirements"></a>프록시 구성 및 요구 사항

같은 구성이 hello 프록시 인프라를 통해 필요한 tooenable 테 넌 트 제한 사항입니다. 이 지침은 일반, 이므로 특정 구현 단계에 대 한 tooyour 프록시 공급 업체의 설명서를 참조 해야 합니다.

#### <a name="prerequisites"></a>필수 조건

- hello 프록시 수 tooperform SSL 인터 셉 션, HTTP 헤더를 삽입 및 Fqdn/Url을 사용 하는 필터 대상 이어야 합니다. 

- 클라이언트는 SSL 통신에 대 한 hello 프록시 제공한 hello 인증서 체인을 신뢰 해야 합니다. 예를 들어 내부 PKI에서 발급 한 인증서를 사용 하면 hello 내부 발급 루트 인증 기관 인증서 신뢰할 수 있어야 합니다.

- 이 기능은 Office 365 구독에 포함 되어 있지만 toouse 테 넌 트 제한 toocontrol tooother SaaS 앱 액세스 하려는 경우 다음 Azure AD Premium 1 라이센스가 필요 합니다.

#### <a name="configuration"></a>구성

각 들어오는 요청 toologin.microsoftonline.com, login.microsoft.com, 및 login.windows.net 두 HTTP 헤더를 삽입: *테를 Restrict 액세스* 및 *Restrict 액세스 직접*합니다.

hello 헤더 hello 요소 다음에 포함 되어야 합니다. 
- 에 대 한 *테를 Restrict 액세스*, 값이 \<테 넌 트 목록 허용\>, 쉼표로 구분 된 목록입니다 tooallow 사용자 tooaccess 원하는 테 넌 트의 합니다. 테 넌 트에 등록 되어 있는 모든 도메인에는이 목록에 사용 되는 tooidentify hello 테 넌 트 될 수 있습니다. 예를 들어 toopermit tooboth Contoso 및 Fabrikam 테 넌 트에 액세스, hello와 같은 이름/값 쌍을 찾습니다.`Restrict-Access-To-Tenants: contoso.onmicrosoft.com,fabrikam.onmicrosoft.com` 
- 에 대 한 *Restrict 액세스 직접*, 테 넌 트 hello 테 넌 트 제한을 설정 하는 것을 선언 하는 단일 디렉터리 ID의 값입니다. 예를 들어 Contoso 테 넌 트 제한 정책 hello를 설정 하는 hello 테 넌 트로 toodeclare hello 이름/값 쌍은 같습니다.`Restrict-Access-Context: 456ff232-35l2-5h23-b3b3-3236w0826f3d`  

> [!TIP]
> Hello에 디렉터리 ID를 찾을 수 [Azure 포털](https://portal.azure.com)합니다. 관리자로 로그인한 후 **Azure Active Directory**를 선택하고 **속성**을 선택합니다.

사용자가 승인 되지 않은 테 넌 트에서 자신의 HTTP 헤더를 삽입할 tooprevent hello 프록시 hello 들어오는 요청에 이미 있으면 tooreplace hello 테를 Restrict 액세스 헤더가 필요 합니다. 

클라이언트는 모든 요청 toologin.microsoftonline.com, login.microsoft.com, 및 login.windows.net 강제 toouse hello 프록시 해야 합니다. 예를 들어 PAC 파일이 사용 되는 toodirect 클라이언트 toouse hello 프록시 경우 최종 사용자가 해야 수 tooedit 또는 수 hello PAC 파일을 사용 하지 않도록 설정.

## <a name="hello-user-experience"></a>hello 사용자 환경

이 섹션에서는 최종 사용자와 관리자 모두에 대 한 hello 환경을 보여 줍니다.

### <a name="end-user-experience"></a>최종 사용자 환경

예제 사용자는 hello Contoso 네트워크에 있지만 공유 SaaS 응용 프로그램의 Outlook 같은 온라인 tooaccess hello Fabrikam 인스턴스를 시도 합니다. Contoso는 해당 인스턴스에 대 한 비 허용 테 넌 트를 하는 경우 다음 페이지 hello hello 사용자에 게 표시:

![허용되지 않는 테넌트의 사용자에 대한 액세스 거부 페이지](./media/active-directory-tenant-restrictions/end-user-denied.png)

### <a name="admin-experience"></a>관리자 환경

Hello 회사 프록시 인프라에서 테 넌 트 제한의 구성이 완료 되, 동안 admins hello 테 넌 트 제한 보고서 hello Azure 포털에에서 직접 액세스할 수 있습니다. tooview hello 보고 toohello Azure Active Directory 개요 페이지에서 다음 '기능 다른' 아래를 확인 합니다.

이 보고서 toosee 사용 되는 hello id를 포함 하 여 테 넌 트 제한 정책을 hello 인해 차단 된 모든 로그인을 사용할 수 있으며 hello 대상 디렉터리의 id입니다. hello 제한 된 액세스 직접 테 넌 트로 지정 된 hello 테 넌 트에 대 한 admin 님 안녕하세요

![Hello 제한 하는 Azure 포털 tooview 로그인 시도 사용 하 여](./media/active-directory-tenant-restrictions/portal-report.png)

Hello Azure 포털에서에서 다른 보고서와 마찬가지로 보고서의 필터 toospecify hello 범위를 사용할 수 있습니다. 특정 사용자, 응용 프로그램, 클라이언트 또는 시간 간격에 따라 필터링을 수행할 수 있습니다.

## <a name="office-365-support"></a>Office 365 지원

Office 365 응용 프로그램 두 조건을 toofully 지원 테 넌 트 제한 사항을 충족 해야 합니다.

1. 사용 되는 hello 클라이언트에서 최신 인증을 지원 합니다.
2. 최신 인증 hello 클라우드 서비스에 대 한 기본 인증 프로토콜이 hello로 사용 됩니다.

너무 참조[업데이트 Office 365 최신 인증](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/) hello 최신 정보를 office 클라이언트 현재 지원 최신 인증에 대 한 합니다. 해당 페이지에는 비즈니스 온라인 테 넌 트에 대 한 특정 Exchange Online 및 Skype에 대 한 최신 인증을 사용 하기 위한 링크 tooinstructions 포함 되어 있습니다. 최신 인증은 기본적으로 SharePoint Online에서 사용되도록 설정됩니다.

테 넌 트 제한은 현재 Office 365 브라우저 기반 응용 프로그램에서 지원 됩니다 (hello Office 포털, Yammer, SharePoint 사이트, Outlook 등 hello 웹.). 씩 클라이언트(Outlook, 비즈니스용 Skype, Word, Excel, PowerPoint 등) 테넌트 제한은 최신 인증을 사용하는 경우에만 적용할 수 있습니다.  

Outlook 및 Skype 최신 인증을 지 원하는 기업 고객은 최신 인증이 설정 되지 않은 테 넌 트에 대해 여전히 수 toouse 레거시 프로토콜을 효과적으로 테 넌 트 제한을 무시 합니다. Windows에서 Outlook에 대 한 고객 tooimplement 제한 사항을 최종 사용자 승인 되지 않은 메일 계정 tootheir 프로필 추가 하는 것을 방지를 선택할 수 있습니다. 예를 들어 hello 참조 [추가 기본이 아닌 Exchange 계정 사용 안 함](http://gpsearch.azurewebsites.net/default.aspx?ref=1) 그룹 정책 설정 합니다. Windows가 아닌 플랫폼의 Outlook과 모든 플랫폼의 비즈니스용 Skype에서는 현재 테넌트 제한을 완벽하게 지원하지 않습니다.

## <a name="testing"></a>테스트

조직에 대 한 구현 하기 전에 테 넌 트 제한 아웃 tootry 하려는 경우 두 가지 옵션이 있습니다: 프록시 설정의 단계별된 롤아웃 또는 Fiddler와 같은 도구를 사용 하는 호스트 기반 접근 방식입니다.

### <a name="fiddler-for-a-host-based-approach"></a>호스트 기반 접근 방식을 위한 Fiddler

Fiddler는 무료 웹 디버깅 프록시 사용된 toocapture 수 및 HTTP/HTTPS 트래픽을, HTTP 헤더를 삽입 하는 포함 하 여 수정할 수 있는 합니다. tooconfigure Fiddler tootest 테 넌 트 제한 hello 다음 단계를 수행 합니다.

1.  [Fiddler 다운로드하고 설치합니다](http://www.telerik.com/fiddler).
2.  Fiddler toodecrypt HTTPS 트래픽을 당 구성 [Fiddler의 도움말 문서](http://docs.telerik.com/fiddler/Configure-Fiddler/Tasks/DecryptHTTPS)합니다.
3.  Fiddler tooinsert hello 구성 *테를 Restrict 액세스* 및 *Restrict 액세스 직접* 사용자 지정 규칙을 사용 하 여 머리글:
  1. Hello Fiddler Web Debugger 도구 선택 hello **규칙** 메뉴와 선택 **규칙 사용자 지정...** tooopen hello CustomRules 파일입니다.
  2. Hello hello hello 맨 앞에 줄을 다음 추가 *OnBeforeRequest* 함수입니다. \<tenant domain\>을 테넌트에 등록된 도메인(예: contoso.onmicrosoft.com)으로 바꿉니다. \<directory ID\>를 테넌트의 Azure AD GUID 식별자로 바꿉니다.

  ```
  if (oSession.HostnameIs("login.microsoftonline.com") || oSession.HostnameIs("login.microsoft.com") || oSession.HostnameIs("login.windows.net")){      oSession.oRequest["Restrict-Access-To-Tenants"] = "<tenant domain>";      oSession.oRequest["Restrict-Access-Context"] = "<directory ID>";}
  ```

  여러 테 넌 트 tooallow 해야 할 경우 쉼표 tooseparate hello 테 넌 트 이름을 사용 합니다. 예:

  ```
  oSession.oRequest["Restrict-Access-To-Tenants"] = "contoso.onmicrosoft.com,fabrikam.onmicrosoft.com";
  ```

4. 저장 하 고 hello CustomRules 파일을 닫습니다.

Fiddler를 구성한 후 toohello 이동 하 여 트래픽을 캡처할 수 있습니다 **파일** 메뉴에서 **트래픽 캡처**합니다.

### <a name="staged-rollout-of-proxy-settings"></a>프록시 설정의 단계별 롤아웃

Hello 프록시 인프라의 기능에 따라 설정 tooyour 사용자의 수 toostage hello 공개 수도 있습니다. 다음은 고려해야 할 몇 가지 고급 옵션입니다.

1.  일반 사용자가 계속 toouse hello 프로덕션 프록시 인프라 PAC 파일 toopoint 테스트 사용자 tooa 테스트 프록시 인프라를 사용 합니다.
2.  일부 프록시 서버는 그룹을 사용하여 다양한 구성을 지원할 수 있습니다.

자세한 내용은 tooyour 프록시 서버 설명서를 참조 하십시오.

## <a name="next-steps"></a>다음 단계

- [업데이트된 Office 365 최신 인증](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/) 참조

- 검토 hello [Office 365 Url 및 IP 주소 범위](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)
