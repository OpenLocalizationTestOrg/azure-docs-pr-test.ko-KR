---
title: "AD FS 인증에 사용 되는 기간 업무 Azure 앱 aaaCreate | Microsoft Docs"
description: "어떻게 toocreate는 기간 업무 앱을 인증 하 고 있는 Azure 앱 서비스의 온-프레미스 STS에 알아봅니다. 이 자습서에는 AD FS 온-프레미스 STS hello으로 대상으로 합니다."
services: app-service\web
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: 0fa9f7a1-37bd-4d11-845f-aeff6fc9e4ca
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: cfd6f14837642fbf58ca5da9dee72db69cd5ab7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a>AD FS 인증을 사용하여 LOB(기간 업무) Azure 앱 만들기
이 문서에서는 어떻게 toocreate는 ASP.NET MVC의 업무 응용 프로그램에서 [Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md) 온-프레미스를 사용 하 여 [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) hello id 공급자로 합니다. 이 시나리오는 toocreate 기간 업무 응용 프로그램을 Azure 앱 서비스의 원하는 었 조직 디렉터리 데이터 toobe 온사이트에 저장에 필요한 경우 사용할 수 있습니다.

> [!NOTE]
> Azure 앱 서비스에 대 한 hello 다른 엔터프라이즈 인증 및 권한 부여 옵션의 개요를 참조 하십시오. [Azure 응용 프로그램에서 온-프레미스 Active Directory로 인증](web-sites-authentication-authorization.md)합니다.
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a>빌드할 내용
같은 기능 hello로 Azure 앱 서비스 웹 앱에서 기본 ASP.NET 응용 프로그램을 작성 합니다.

* AD FS에 대해 사용자 인증
* 사용 하 여 `[Authorize]` 다양 한 작업에 대 한 tooauthorize 사용자
* Visual Studio에서 디버깅와 tooApp 서비스 웹 앱 게시에 대 한 고정 구성을 (한 번의 구성, 디버깅 및 게시를 언제 든 지)  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a>필요한 항목
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

이 자습서 toocomplete 다음 hello 필요:

* 온-프레미스 AD FS 배포 (이 자습서에 사용 된 hello 테스트 랩의 종단 간 연습을 참조 하십시오. [테스트 랩: (테스트에만 해당)에 대 한 Azure VM의 AD FS와 함께 독립 실행형 STS](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))
* 사용 권한 toocreate 신뢰 당사자 트러스트가 AD FS 관리 있습니다
* Visual Studio 2013 업데이트 4 이상
* [Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) 이상

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a>기간 업무 템플릿에 예제 응용 프로그램 사용
이 자습서에서는 샘플 응용 프로그램 hello [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), hello Azure Active Directory 팀에서 만들어집니다. AD FS Ws-federation을 지 원하는 하므로 손쉽게 템플릿 toocreate 기간 업무 응용 프로그램으로 사용할 수 있습니다. 같은 기능 hello 다음과 같습니다.

* 사용 하 여 [WS-페더레이션](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate 온-프레미스 AD FS 배포
* 로그인 및 로그아웃 기능
* 사용 하 여 [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (Windows Identity Foundation)를 대신 하는 hello ASP.NET 및 WIF 보다 인증 및 권한 부여에 대해 훨씬 더 간단 tooset의 이후

<a name="bkmk_setup"></a>

## <a name="set-up-hello-sample-application"></a>Hello 샘플 응용 프로그램 설정
1. 복제 또는에 hello 샘플 솔루션 다운로드 [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour 로컬 디렉터리입니다.
   
   > [!NOTE]
   > 지침에 hello [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) 방법을 보여 줍니다 tooset Azure Active Directory와 hello 응용 프로그램을 설치 합니다. 하지만이 자습서에서는 AD FS를 사용 하 여 설정 하면,이 따라서 대신 hello 단계를 수행 합니다.
   > 
   > 
2. Hello 솔루션을 연 다음 Controllers\AccountController.cs hello에 **솔루션 탐색기**합니다.
   
   Hello 코드에 단순히 Ws-federation을 사용 하는 인증 챌린지 tooauthenticate hello 사용자 문제를 확인할 수 있습니다. 모든 인증은 App_Start\Startup.Auth.cs에서 구성됩니다.
3. App_Start\Startup.Auth.cs를 엽니다. Hello에 `ConfigureAuth` 메서드, 참고 hello 줄:
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   Hello OWIN 환경에서이 코드 조각은 실제로 hello tooconfigure WS-페더레이션 인증 필요한 최소 운영 체제 미 설치입니다. 것이 훨씬 쉽고 hello 장소 전 세계 Web.config XML로 주입 여기서 WIF 보다 더 적합 합니다. 필요한 정보 hello의 RP (신뢰 당사자) 파일인 hello AD FS 서비스의 메타 데이터 파일의 URL 식별자 및 hello 합니다. 예를 들면 다음과 같습니다.
   
   * RP 식별자: `https://contoso.com/MyLOBApp`
   * 메타데이터 주소: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`
4. App_Start\Startup.Auth.cs, hello 다음 정적 문자열 정의 변경 합니다.  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. Web.config의 hello 해당 변경 내용을 확인 합니다. Hello Web.config를 열고 hello 다음 응용 프로그램 설정을 수정 합니다.  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter hello App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter hello relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter hello FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   해당 환경에 따라 hello 키 값을 입력 합니다.
6. 오류가 없는 있는지 hello 응용 프로그램 toomake를 빌드하십시오.

이것으로 끝입니다. 이제 hello 샘플 응용 프로그램은 AD FS와 함께 준비 toowork 합니다. 이 응용 프로그램으로 AD FS에서 나중에 RP trust tooconfigure를 보내야합니다.

<a name="bkmk_deploy"></a>

## <a name="deploy-hello-sample-application-tooazure-app-service-web-apps"></a>Hello 샘플 응용 프로그램 tooAzure 앱 서비스 웹 앱 배포
여기에서는 있습니다 hello 응용 프로그램 tooa web app을 게시 앱 서비스 웹 앱에서 hello 디버그 환경 유지 하면서 합니다. Note 하 겠 군요 toopublish hello 응용 프로그램 인증 여전히 작동 하지 않으면 아직 하므로 RP trust AD FS와 함께 갖기 전에 합니다. 그러나 이렇게 하면 이제 가질 수 있습니다 tooconfigure hello RP trust을 나중에 사용할 수 있는 hello 웹 앱 URL입니다.

1. 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. **Microsoft Azure 앱 서비스**를 선택합니다.
3. TooAzure에 서명 하지 않은 경우 클릭 **로그인** 에 Azure 구독 toosign 프로그램에 대 한 hello Microsoft 계정을 사용 합니다.
4. 로그인 한 후 클릭 **새로** toocreate 웹 앱입니다.
5. 모든 필수 필드를 입력합니다. 하려고 tooconnect tooon 온-프레미스 데이터 나중 하므로이 웹 앱에 대 한 데이터베이스를 만들지 않습니다.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. **만들기**를 클릭합니다. Hello 웹 응용 프로그램을 만든 후에 hello 웹 게시 대화 상자를 열면 됩니다.
7. **대상 URL**, 변경 **http** 너무**https**합니다. 복사 hello 전체 URL tooa 텍스트 편집기 나중에 사용할 수 있습니다. 그런 다음 **게시**를 클릭합니다.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. Visual Studio에서 프로젝트의 **Web.Release.config** 를 엽니다. Hello에 다음과 같은 XML hello 삽입 `<configuration>` 태그, 및 hello 키 값을 게시 웹 앱의 URL로 바꿉니다.  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

완료 되 면 Visual Studio에서 디버그 환경에 대 한 프로젝트에 구성 된 두 개의 RP 식별자가 있으며 Azure에서 웹 앱을 게시 한 hello에 대 한 합니다. 각 AD FS에서 두 가지 환경 hello에 대 한 RP 트러스트를 설정 합니다. 디버깅 하는 동안 hello 응용 프로그램의 Web.config 설정이 사용 되는 toomake 프로그램 **디버그** AD FS와 함께 구성 작업입니다. 게시 되는 경우 (기본적으로 hello **릴리스** 구성 게시), 통합 hello Web.Release.config에 응용 프로그램은 설정을 변경 하는 변환 된 Web.config 업로드 됩니다.

Hello의 복제본을 만들 수 있습니다, (예: hello 게시 된 웹 앱에서 코드의 디버그 기호를 업로드 해야 합니다) Azure toohello 디버거에서 디버그, 디버깅 하는 Azure에 대 한 구성 하지만 고유한 사용자 지정 Web.config 사용 (변환할 tooattach hello 게시 된 웹 앱에 포함 하려는 경우 예를 들어 Web.AzureDebug.config) Web.Release.config에서 응용 프로그램 설정을 hello를 사용 하 합니다. 이렇게 하면 있습니다 toomaintain 고정 구성을 hello 서로 다른 환경에서.

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a>AD FS 관리에서 신뢰 당사자 트러스트 구성
이제 있어야만 tooconfigure는 RP trust AD FS 관리에서 샘플 응용 프로그램을 사용 하 고 AD FS와 함께 실제로 인증할 수 있습니다. 디버그 환경 및 게시 된 웹 앱에 대 한 두 개의 별도 RP 트러스트를 tooset 필요 합니다.

> [!NOTE]
> Hello 사용자 환경의 둘 다에 대해 다음 단계를 반복 하 고 있는지 확인 합니다.
> 
> 

1. AD FS 서버에서 관리 권한 tooAD FS 권한이 있는 자격 증명으로 로그인 합니다.
2. AD FS 관리를 엽니다. **AD FS\Trusted Relationships\Relying Party Trusts**를 마우스 오른쪽 단추로 클릭하고 **신뢰 당사자 트러스트 추가**를 선택합니다.
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. Hello에 **데이터 원본 선택** 페이지 **hello 신뢰 당사자에 대 한 데이터를 직접 입력**합니다. 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. Hello에 **표시 이름 지정** 페이지 hello 응용 프로그램에 대 한 표시 이름을 입력 하 고 클릭 **다음**합니다.
5. Hello에 **프로토콜 선택** 페이지 **다음**합니다.
6. Hello에 **인증서 구성** 페이지 **다음**합니다.
   
   > [!NOTE]
   > HTTPS를 이미 사용하고 있으므로 암호화된 토큰은 선택 사항입니다. 이 페이지에서 AD FS에서 tooencrypt 토큰을 원하는 경우에 코드에도 토큰 암호 해독 논리를 추가할 해야 합니다. 자세한 내용은 [OWIN WS-Federation 미들웨어를 수동으로 구성하고 암호화된 토큰 적용](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx)을 참조하세요.
   > 
   > 
7. Hello 다음 단계로 이동 하기 전에 Visual Studio 프로젝트에서 하나의 필요 합니다. Hello 프로젝트 속성에서 확인 hello **SSL URL** hello 응용 프로그램의 합니다. 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. Hello에 AD FS 관리에 다시 **URL 구성** hello 페이지 **신뢰 당사자 트러스트 추가 마법사**선택, **hello Ws-federation 수동 프로토콜 지원 사용** 및 hello 이전 단계에서 기록해둔 hello Visual Studio 프로젝트의 SSL URL에에서 입력 합니다. 그런 후 **다음**을 클릭합니다.
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > URL은 toosend hello 클라이언트 인증이 성공 하면를 지정 합니다. Hello 디버그 환경에 대 한 것 <code>https://localhost:&lt;port&gt;/</code>합니다. Hello 게시 된 웹 앱에 대 한 hello 웹 앱 URL 이어야 합니다.
   > 
   > 
9. Hello에 **식별자 구성** 페이지 SSL URL을 프로젝트에 이미 나열 되어 있는지 확인 하 고 클릭 **다음**합니다. 클릭 **다음** 기본 선택 항목으로 hello 마법사의 방식으로 toohello 마지막 hello 모든 합니다.
   
   > [!NOTE]
   > Visual Studio 프로젝트의 App_Start\Startup.Auth.cs에서이 식별자는 일치의 hello 값 <code>WsFederationAuthenticationOptions.Wtrealm</code> 페더레이션된 인증 하는 동안 합니다. 기본적으로 hello 이전 단계의 hello 응용 프로그램의 URL은 RP 식별자로 추가 됩니다.
   > 
   > 
10. 이제 AD FS에서 hello RP 응용 프로그램 프로젝트에 대 한 구성 작업이 완료 되었습니다. 이제이 응용 프로그램 toosend 구성 hello 클레임 응용 프로그램에 필요 합니다. hello **클레임 규칙 편집** 대화 상자가 열려 기본적으로 사용자에 대 한 hello 마법사 hello 끝나기 전에 즉시 시작할 수 있도록 합니다. 구성 (스키마와 함께 괄호 안에 있음) 클레임 다음 hello 이상:
    
    * ASP.NET toohydrate에서 사용 하는 이름 (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name)- `User.Identity.Name`합니다.
    * 사용자 계정 이름 (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn)-사용 되는 toouniquely hello 조직에서 사용자를 식별 합니다.
    * 와 함께 사용할 수 역할로 (http://schemas.microsoft.com/ws/2008/06/identity/claims/role)-그룹 구성원 자격 `[Authorize(Roles="role1, role2,...")]` 장식 tooauthorize 컨트롤러/작업 합니다. 실제로이 방법을 사용 될 수 있습니다 되지 수 hello 역할 권한 부여에 대 한 대부분 고성능 합니다. AD 사용자가 속하는 보안 그룹의 toohundreds, 수백 hello SAML 토큰에서 역할 클레임의 되 됩니다. 또 다른 방법은 단일 역할 hello 사용자의 특정 그룹 구성원 자격에 따라 조건부로 클레임 toosend 합니다. 하지만 이 자습서에서는 이 접근 방식을 단순한 형태로 제공합니다.
    * 이름 ID(http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier)는 위조 방지 유효성 검사를 위해 사용될 수 있습니다. 어떻게 toomake 작동 위조 방지 유효성 검사에 대 한 자세한 내용은 참조 hello **기간 업무 기능을 추가할** 의 섹션 [Azure Active Directory 인증으로 업무의 Azure 응용 프로그램 만들기 ](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).
    
    > [!NOTE]
    > hello 클레임 형식에 응용 프로그램은 응용 프로그램의 요구 사항에 따라 결정 tooconfigure 필요 합니다. Azure Active Directory 응용 프로그램 (즉, RP 트러스트)에서 지원 되는 클레임의 hello 목록에 대 한 예를 들어 참조 [지원 되는 토큰 및 클레임 유형](http://msdn.microsoft.com/library/azure/dn195587.aspx)합니다.
    > 
    > 
11. Hello 클레임 규칙 편집 대화 상자에서 **규칙 추가**합니다.
12. Hello 스크린샷에 표시 된 대로 hello 이름, UPN 및 역할 클레임을 구성 하 고 클릭 **마침**합니다.
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    다음으로 일시적인 이름 ID 클레임에서 보여 준 hello 단계를 사용 하 여 만듭니다 [SAML 어설션 식별자 이름](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx)합니다.
13. **규칙 추가** 를 다시 클릭합니다.
14. **사용자 지정 규칙을 사용하여 클레임 보내기**를 선택하고 **다음**을 클릭합니다.
15. 붙여넣기 hello 다음 hello에 언어 규칙 **사용자 지정 규칙** 상자, 이름 hello 규칙 **세션 식별자 당** 클릭 **마침**합니다.  
    
    <pre class="prettyprint">
    c1:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"] &amp;&amp;
    c2:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant"]
     => add(
         store = "_OpaqueIdStore",
         types = ("<mark>http://contoso.com/internal/sessionid</mark>"),
         query = "{0};{1};{2};{3};{4}",
         param = "useEntropy",
         param = c1.Value,
         param = c1.OriginalIssuer,
         param = "",
         param = c2.Value);
    </pre>
    
    사용자 지정 규칙은 이 스크린샷과 같습니다.
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. **규칙 추가** 를 다시 클릭합니다.
17. **들어오는 클레임 변환**을 선택하고 **다음**을 클릭합니다.
18. (Hello 사용자 지정 규칙에서 만든 hello 클레임 유형을 사용 하 여) hello 스크린샷에 표시 된 대로 hello 규칙을 구성 하 고 클릭 **마침**합니다.
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    Hello 일시적인 이름 ID 클레임에 대 한 hello 단계에 대 한 자세한 내용은 참조 하십시오. [SAML 어설션 식별자 이름](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx)합니다.
19. 클릭 **적용** hello에 **클레임 규칙 편집** 대화 상자. 이 파일은 이제 같아야 스크린 샷 다음 hello:
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > 즉, 디버그 환경과 게시된 웹 앱 둘 다에 대해 이러한 단계를 반복해야 합니다.
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a>응용 프로그램에 대한 페더레이션 인증 테스트
사용자는 준비 tootest AD FS에 대 한 응용 프로그램의 인증 논리입니다. 내 AD FS 랩 환경에서 tooa 테스트 그룹에 AD (Active Directory)에 속하는 테스트 사용자를 있습니다.

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

하기만 하면 toodo 이제 hello 디버거에서 tootest 인증 형식이 `F5`합니다. Hello 게시 된 웹 응용 프로그램에서 tootest 인증 하려는 경우 toohello URL을 탐색 합니다.

Hello 웹 응용 프로그램에 로드 된 후 클릭 **로그인**합니다. 이제 중 하나는 로그인 대화 상자 또는 hello 로그인 페이지에 AD FS에서 선택한 hello 인증 방법에 따라 AD FS을 구해야 합니다. 다음은 Internet Explorer 11의 화면 예입니다.

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

사용 하 여 다시 hello 홈 페이지 이제 표시 hello AD FS 배포의 hello AD 도메인에서 사용자를 사용 하 여 로그온 한 후 **Hello, <User Name>!** hello 구석에 합니다. 예를 들면 다음과 같습니다.

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

지금까지 다음 방법으로 hello 성공:

* 응용 프로그램에 AD FS를 성공적으로 도달 하 고 hello AD FS 데이터베이스에서에서 일치 하는 RP 식별자를 찾을 수합니다
* AD FS에는 AD 사용자 및 toohello 응용 프로그램의 홈 페이지를 다시 리디렉션 성공적으로 인증 된
* 해당 hello 사용자 hello 팩트에 표시 된 대로 성공적으로 보낸된 hello 이름으로 AD FS 클레임 (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) tooyour 응용 프로그램 이름이 hello 모서리에 표시 됩니다. 

Hello 이름 클레임이 없는 경우 했겠지만 **Hello,!**합니다. Views\Shared 보면\_사용 하는 것을 찾을 LoginPartial.cshtml, `User.Identity.Name` toodisplay hello 사용자 이름입니다. Hello 이름 hello SAML 토큰에서 사용할 수 있는 사용자가 인증 된 hello의 청구 하는 경우 이전에 언급 했 듯이 ASP.NET hydrates 함께이 속성입니다. 모든 hello toosee Index 작업 메서드의 hello에서 Controllers\HomeController.cs에 중단점을 배치 하는 AD FS에서 전송 된 클레임입니다. Hello 사용자가 인증 되 면 hello 검사 `System.Security.Claims.Current.Claims` 컬렉션입니다.

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a>사용자에게 특정 컨트롤러 또는 작업에 대한 권한 부여
RP 신뢰 구성에서 역할 클레임으로 그룹 멤버 자격을 포함 한, 있으므로 이제 사용할 수 있습니다 이러한 hello에 직접 `[Authorize(Roles="...")]` 컨트롤러 및 작업에 대 한 장식 합니다. Hello 만들기-읽기-업데이트-삭제 (CRUD) 패턴으로 기간 업무 응용 프로그램에서는 특정 역할 tooaccess 각 동작을 인증할 수 있습니다. 이제 방금 hello 기존 홈 컨트롤러에이 기능을 미리 시도 합니다.

1. Controllers\HomeController.cs를 엽니다.
2. Hello 데코레이팅 `About` 및 `Contact` 동작 메서드 비슷한 toohello 코드 다음, 인증 된 사용자가 보안 그룹 구성원 자격을 사용 하 여 합니다.  
   
    <pre class="prettyprint">
    <mark>[Authorize(Roles="Test Group")]</mark>
    public ActionResult About()
    {
        ViewBag.Message = "Your application description page.";
   
        return View();
    }
   
    <mark>[Authorize(Roles="Domain Admins")]</mark>
    public ActionResult Contact()
    {
        ViewBag.Message = "Your contact page.";
   
        return View();
    }
    </pre>
   
    추가한 이후 **테스트 사용자** 너무**테스트 그룹** 내 AD FS 랩 환경에서 테스트 그룹 tootest 권한 부여에 사용 합니다 I `About`합니다. 에 대 한 `Contact`의 hello 음수일 경우 테스트할 **Domain Admins**, toowhich **테스트 사용자** 속해 있지 않습니다.
3. 입력 하 여 hello 디버거를 시작 `F5` 로그인 하 고 다음 클릭 **에 대 한**합니다. 지금 표시할 수 있습니다 hello `~/About/Index` 페이지 성공적으로 인증 된 사용자가 해당 작업에 대 한 권한을 부여 하는 경우.
4. 클릭 하 여 지금 **연락처**, 여기서에서는 승인 하지 해야 **테스트 사용자** hello 동작에 대 한 합니다. 그러나 hello 브라우저 리디렉션된 tooAD FS, 결국이 메시지를 표시 하는 것입니다.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    AD FS 서버 hello에 이벤트 뷰어에서이 오류를 조사 하는 경우이 예외 메시지가 표시 됩니다.  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>hello same client browser session has made '6' requests in hello last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    이 오류에 대 한 hello 이유는 기본적으로 MVC 반환 401 권한 없음 사용자 역할은 권한이 없는 경우는입니다. 재인증 요청 tooyour id 공급자를 (AD FS)를 트리거합니다. Hello 사용자가 이미 인증 AD FS toohello 반환 같은 페이지에서 리디렉션 루프를 작성 하는 다른 401을 발급 합니다. AuthorizeAttribute의 대체 `HandleUnauthorizedRequest` 간단한 논리 tooshow 사용 메서드를 계속 hello 리디렉션 루프 대신 의미가 있는 합니다.
5. AuthorizeAttribute.cs, 및 코드를 다음 붙여넣기 hello 라는 hello 프로젝트에서 파일을 만듭니다.
   
        using System;
        using System.Web.Mvc;
        using System.Web.Routing;
   
        namespace WebApp_WSFederation_DotNet
        {
            [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
            public class AuthorizeAttribute : System.Web.Mvc.AuthorizeAttribute
            {
                protected override void HandleUnauthorizedRequest(AuthorizationContext filterContext)
                {
                    if (filterContext.HttpContext.Request.IsAuthenticated)
                    {
                        filterContext.Result = new System.Web.Mvc.HttpStatusCodeResult((int)System.Net.HttpStatusCode.Forbidden);
                    }
                    else
                    {
                        base.HandleUnauthorizedRequest(filterContext);
                    }
                }
            }
        }
   
    hello 코드 보냅니다 HTTP 403 (금지 됨) HTTP 401 (권한 없음) 하는 대신 인증 된 하지만 권한이 없는 경우에서를 재정의 합니다.
6. 사용 하 여 다시 hello 디버거 실행 `F5`합니다. 이제 **Contact** 를 클릭하면 보다 자세한(중요하지는 않음) 오류 메시지가 표시됩니다.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. Hello 응용 프로그램 tooAzure 앱 서비스 웹 앱을 다시 게시 하 고 hello 라이브 응용 프로그램의 hello 동작을 테스트 합니다.

<a name="bkmk_data"></a>

## <a name="connect-tooon-premises-data"></a>Tooon 온-프레미스 데이터 연결
Tooimplement AD fs를 Azure Active Directory 대신 기간 업무 응용 프로그램을 사용할 수 있는지는 이유는 조직의 데이터 오프-프레미스를 유지 하는 규정 준수 문제입니다. Toouse 수 있으므로 Azure에서 웹 앱이 온-프레미스 데이터베이스를 액세스 해야 또한 것일 [SQL 데이터베이스](/services/sql-database/) 웹 앱에 대 한 hello 데이터 계층입니다.

Azure App Service Web Apps는 [하이브리드 연결](../biztalk-services/integration-hybrid-connection-overview.md) 및 [가상 네트워크](web-sites-integrate-with-vnet.md)의 두 가지 방법으로 온-프레미스 데이터베이스 액세스를 지원합니다. 자세한 내용은 [Azure App Service Web Apps에서 VNET 통합 및 하이브리드 연결 사용](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/)을 참조하세요.

<a name="bkmk_resources"></a>

## <a name="further-resources"></a>추가 리소스
* [Azure 앱에서 온-프레미스 Active Directory를 사용하여 인증](web-sites-authentication-authorization.md)
* [Azure Active Directory 인증을 사용하여 LOB(기간 업무) Azure 앱 만들기](web-sites-dotnet-lob-application-azure-ad.md)
* [Visual Studio 2013에서 온-프레미스 조직 인증 옵션 (ADFS)으로 ASP.NET hello를 사용 하 여](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [VS2013 웹 프로젝트에서 WIF tooKatana 마이그레이션](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [Active Directory Federation Services 개요](http://technet.microsoft.com/library/hh831502.aspx)
* [WS-Federation 1.1 사양](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

