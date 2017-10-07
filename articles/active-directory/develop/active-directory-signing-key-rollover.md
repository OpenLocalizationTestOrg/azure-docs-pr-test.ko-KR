---
title: "Azure AD에서 키 롤오버 aaaSigning | Microsoft Docs"
description: "이 문서에서는 Azure Active Directory에 대 한 키 롤오버에 대 한 유용한 정보를 서명 하는 hello 설명"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: krassk
editor: 
ms.assetid: ed964056-0723-42fe-bb69-e57323b9407f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ac6ade7f3ba2fbd22ea6d447aa5d07a2d6bdd451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a>Azure Active Directory에서 서명 키 롤오버
이 항목에서는 Azure Active Directory (Azure AD) toosign 보안 토큰에 사용 되는 공개 키를 hello에 대 한 tooknow 필요한 설명 합니다. 것이 중요 한 toonote는 주기적으로 및를 긴급 상황에서는 이러한 키 롤오버를 통해 즉시 롤백할 수 없습니다. Azure AD를 사용 하는 모든 응용 프로그램 수 tooprogrammatically 핸들 hello 키 롤오버 프로세스 하거나 정기적으로 수동 롤오버 프로세스를 설정 해야 합니다. Hello 키가 작동 방식을 tooassess hello hello 롤오버 tooyour 응용 프로그램에 미치는 방식과 toounderstand 읽고 tooupdate 응용 프로그램, 필요한 경우 정기적으로 수동 롤오버 프로세스 toohandle 키 롤오버를 설정할 합니다.

## <a name="overview-of-signing-keys-in-azure-ad"></a>Azure AD의 서명 키 개요
Azure AD는 업계 표준 tooestablish 트러스트 자체와 hello 사이 작성 된 공개 키 암호화를 사용을 사용 하는 응용 프로그램입니다. 실질적으로 보안 그룹은 다음 방식으로 hello: Azure AD는 공개 및 개인 키 쌍으로 구성 된 서명 키를 사용 합니다. 사용자 인증을 위해 Azure AD를 사용 하는 tooan 응용 프로그램에 로그인 하면 Azure AD는 hello 사용자에 대 한 정보를 포함 하는 보안 토큰을 만듭니다. 이 토큰은 응용 프로그램 백 toohello 전송 하기 전에 해당 개인 키를 사용 하 여 Azure AD에서 서명 됩니다. 토큰 hello tooverify가 유효 하 고 실제로 Azure AD에서 공개한, hello 응용 프로그램 hello hello 테 넌 트에 포함 된 Azure AD에 의해 노출 되는 공개 키를 사용 하 여 hello 토큰 서명의 유효성을 검사 해야 [검색 문서 OpenID Connect](http://openid.net/specs/openid-connect-discovery-1_0.html) 또는 SAML/Ws-fed [페더레이션 메타 데이터 문서](active-directory-federation-metadata.md)합니다.

보안을 위해 Azure AD의 서명 키 롤 주기적으로 고, 비상 시 hello 경우에서 수 롤오버 즉시 합니다. Azure AD와 통합 되어 있는 모든 응용 프로그램 키 롤오버 이벤트 발생할 수 있는 빈도 관계 없이 toohandle를 준비 해야 합니다. 그렇지 않은 경우 응용 프로그램 토큰에는 만료 된 키 tooverify hello 서명 toouse 시도 hello 로그인 요청이 실패 합니다.

항상 둘 이상의 유효한 키가 hello OpenID Connect 검색 문서 및 hello 페더레이션 메타 데이터 문서에서 사용할 수 있습니다. 응용 프로그램을 준비 해야 toouse hello 키에 지정 된 hello 문서 키가 두 개를 곧 롤오버 될 수 있으므로 다른를 대체할 하 고 등 수 있습니다.

## <a name="how-tooassess-if-your-application-will-be-affected-and-what-toodo-about-it"></a>어떻게 응용 프로그램이 영향을 받을 경우 tooassess 및 항목에 대 한 어떤 toodo
응용 프로그램에서 키 롤오버를 처리 하는 방법에 따라 다름 hello 유형의 응용 프로그램이 나 어떤 identity 프로토콜 및 라이브러리를 사용 하는 등의 변수 아래 섹션에서는 hello hello 가장 일반적인 유형의 응용 프로그램 hello 키 롤오버의 영향을 받는 방법을 tooupdate 응용 프로그램 toosupport 자동 롤오버 hello 또는 hello 키를 수동으로 업데이트 한 지침을 제공 하는지 여부를 평가 합니다.

* [리소스에 액세스하는 네이티브 클라이언트 응용 프로그램](#nativeclient)
* [리소스에 액세스하는 웹 응용 프로그램/API](#webclient)
* [리소스를 보호하고 Azure 앱 서비스를 사용하여 구축된 웹 응용 프로그램/API](#appservices)
* [.NET OWIN OpenID Connect, WS-Fed 또는 WindowsAzureActiveDirectoryBearerAuthentication 미들웨어를 사용하여 리소스를 보호하는 웹 응용 프로그램/API](#owin)
* [.NET Core OpenID Connect 또는 JwtBearerAuthentication 미들웨어를 사용하여 리소스를 보호하는 웹 응용 프로그램/API](#owincore)
* [Node.js passport-azure-ad 모듈을 사용하여 리소스를 보호하는 웹 응용 프로그램/API](#passport)
* [리소스를 보호하며 Visual Studio 2015 또는 Visual Studio 2017을 사용하여 만든 웹 응용 프로그램/API](#vs2015)
* [리소스를 보호하며 Visual Studio 2013을 사용하여 만든 웹 응용 프로그램](#vs2013)
* [리소스를 보호하며 Visual Studio 2013을 사용하여 만든 웹 API](#vs2013_webapi)
* [리소스를 보호하며 Visual Studio 2012를 사용하여 만든 웹 응용 프로그램](#vs2012)
* [리소스를 보호하며 Visual Studio 2010, 2008 또는 WIF(Windows Identity Foundation)를 사용하여 만든 웹 응용 프로그램](#vs2010)
* [웹 응용 프로그램/리소스를 보호 하는 Api를 사용 하 여 다른 라이브러리 또는 수동으로 구현 하는 hello의 지원 되는 프로토콜](#other)

이 설명서는 다음에 적용할 수 **없습니다** .

* (사용자 정의 포함)는 Azure AD 응용 프로그램 갤러리에서 추가 하는 응용 프로그램에 대 한 예정 toosigning 키를 가진 별도 지침이 있습니다. [자세한 정보](../active-directory-sso-certs.md)
* 온-프레미스 응용 프로그램 프록시를 통해 게시 된 응용 프로그램 서명 키에 대 한 tooworry 필요는 없습니다.

### <a name="nativeclient"></a>리소스에 액세스하는 네이티브 클라이언트 응용 프로그램
리소스에만 액세스하는 응용 프로그램(즉, Microsoft Graph, KeyVault, Outlook API 및 다른 Microsoft Api) 일반적으로 토큰을 가져올 및만 toohello 리소스 소유자를 따라 전달 합니다. 모든 리소스를 보호 하지 않습니다, 있다고 가정 hello 토큰을 검사 하지 않는 하며 따라서 tooensure 올바르게 서명은 필요 하지 않습니다.

네이티브 클라이언트 응용 프로그램 데스크톱 또는 모바일,이 범주에 속하는 하 고 따라서 영향을 받지 않습니다 hello 롤오버 합니다.

### <a name="webclient"></a>리소스에 액세스하는 웹 응용 프로그램/API
리소스에만 액세스하는 응용 프로그램(즉, Microsoft Graph, KeyVault, Outlook API 및 다른 Microsoft Api) 일반적으로 토큰을 가져올 및만 toohello 리소스 소유자를 따라 전달 합니다. 모든 리소스를 보호 하지 않습니다, 있다고 가정 hello 토큰을 검사 하지 않는 하며 따라서 tooensure 올바르게 서명은 필요 하지 않습니다.

웹 응용 프로그램 및 웹 응용 프로그램 전용 흐름 hello를 사용 하는 Api (클라이언트 자격 증명 / 클라이언트 인증서)이이 범주에 해당 하 고 따라서 영향을 받지 않습니다 hello 롤오버 합니다.

### <a name="appservices"></a>리소스를 보호하고 Azure 앱 서비스를 사용하여 구축된 웹 응용 프로그램/API
Azure 앱 서비스의 인증 / 권한 부여 (EasyAuth) 기능에 이미 키 롤오버를 toohandle hello 필수 논리가 자동으로 합니다.

### <a name="owin"></a>.NET OWIN OpenID Connect, WS-Fed 또는 WindowsAzureActiveDirectoryBearerAuthentication 미들웨어를 사용하여 리소스를 보호하는 웹 응용 프로그램/API
응용 프로그램에서.NET OWIN OpenID Connect, Ws-fed 또는 WindowsAzureActiveDirectoryBearerAuthentication 미들웨어 hello를 사용 하는 경우 이미 키 롤오버를 toohandle hello 필수 논리가 자동으로 합니다.

응용 프로그램이 응용 프로그램의 Startup.cs 또는 Startup.Auth.cs 코드 조각은 다음 hello에 대 한 검색 하 여 이러한 항목 중 하나를 사용 중인지 확인할 수 있습니다.

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseWsFederationAuthentication(
    new WsFederationAuthenticationOptions
    {
     // ...
     });
```
```
 app.UseWindowsAzureActiveDirectoryBearerAuthentication(
     new WindowsAzureActiveDirectoryBearerAuthenticationOptions
     {
     // ...
     });
```

### <a name="owincore"></a>.NET Core OpenID Connect 또는 JwtBearerAuthentication 미들웨어를 사용하여 리소스를 보호하는 웹 응용 프로그램/API
응용 프로그램은.NET Core OWIN OpenID Connect hello 또는 JwtBearerAuthentication 미들웨어를 사용 하는 경우 이미 키 롤오버를 toohandle hello 필수 논리가 자동으로 합니다.

응용 프로그램이 응용 프로그램의 Startup.cs 또는 Startup.Auth.cs 코드 조각은 다음 hello에 대 한 검색 하 여 이러한 항목 중 하나를 사용 중인지 확인할 수 있습니다.

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseJwtBearerAuthentication(
    new JwtBearerAuthenticationOptions
    {
     // ...
     });
```

### <a name="passport"></a>Node.js passport-azure-ad 모듈을 사용하여 리소스를 보호하는 웹 응용 프로그램/API
응용 프로그램 hello Node.js passport ad 모듈을 사용 하는 경우 이미 키 롤오버를 toohandle hello 필수 논리가 자동으로 합니다.

되는지 확인할 수 있습니다 다음 응용 프로그램의 app.js의 조각 hello에 대 한 검색 하 여 응용 프로그램 passport ad 프로그램

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <a name="vs2015"></a>리소스를 보호하며 Visual Studio 2015 또는 Visual Studio 2017을 사용하여 만든 웹 응용 프로그램/API
Visual Studio 2015 또는 Visual Studio 2017에서 웹 응용 프로그램 템플릿을 사용 하 여 응용 프로그램을 빌드한 경우 선택한 **작업 및 학교 계정** hello에서 **인증 변경** 메뉴 이미 hello 필수 논리가 toohandle 키 롤오버를 자동으로 부여 합니다. Hello OpenID Connect OWIN 미들웨어에 포함 된이 논리를 검색 및 hello OpenID Connect 검색 문서에서 hello 키를 캐시 하 고 주기적으로 새로 고쳐집니다.

인증 tooyour 솔루션을 수동으로 추가 하는 경우 응용 프로그램에서는 hello 필수 키 롤오버 논리가 없을 수 있습니다. Toowrite 필요 합니다 것의 단계를 직접 또는 따라 hello [웹 응용 프로그램 / Api 수동으로 hello 중 하나를 구현 하거나 다른 라이브러리를 사용 하 여 프로토콜을 지원 합니다.](#other)합니다.

### <a name="vs2013"></a>리소스를 보호하며 Visual Studio 2013을 사용하여 만든 웹 응용 프로그램
Visual Studio 2013에서 웹 응용 프로그램 템플릿을 사용 하 여 응용 프로그램을 빌드한 경우 선택한 **조직 계정** hello에서 **인증 변경** 메뉴 이미 hello 필요 키 롤오버를 자동으로 논리 toohandle 합니다. 이 논리는 조직의 고유 식별자 및 hello 프로젝트와 관련 된 두 개의 데이터베이스 테이블에 키 정보를 서명 하는 hello를 저장 합니다. Hello 프로젝트의 Web.config 파일에 hello 데이터베이스에 대 한 hello 연결 문자열을 찾을 수 있습니다.

인증 tooyour 솔루션을 수동으로 추가 하는 경우 응용 프로그램에서는 hello 필수 키 롤오버 논리가 없을 수 있습니다. Toowrite 필요 합니다 것의 단계를 직접 또는 따라 hello [웹 응용 프로그램 / Api 수동으로 hello 중 하나를 구현 하거나 다른 라이브러리를 사용 하 여 프로토콜을 지원 합니다.](#other)합니다.

단계를 수행 하는 hello hello 논리가 응용 프로그램에서 제대로 작동 하는지 확인 하는 데 도움이 됩니다.

1. Visual Studio 2013에서 hello 솔루션을 열고 hello에 클릭 **서버 탐색기** hello 오른쪽 창에 탭 합니다.
2. **데이터 연결**, **DefaultConnection**, **테이블**을 차례로 확장합니다. Hello 찾을 **IssuingAuthorityKeys** 테이블을 마우스 오른쪽 단추로 클릭 하 고 클릭 **테이블 데이터 표시**합니다.
3. Hello에 **IssuingAuthorityKeys** 테이블, hello 키에 대 한 toohello 지문 값을 해당 하는 하나 이상의 행이 생깁니다. Hello 테이블의 모든 행을 삭제 합니다.
4. 마우스 오른쪽 단추로 클릭 hello **테 넌 트** 테이블을 마우스 클릭 **테이블 데이터 표시**합니다.
5. Hello에 **테 넌 트** 테이블, 해당 tooa 고유한 디렉터리 테 넌 트 식별자는 하나 이상의 행이 생깁니다. Hello 테이블의 모든 행을 삭제 합니다. 두 hello의 hello 행을 삭제 하지 않으면 **테 넌 트** 테이블 및 **IssuingAuthorityKeys** 테이블을 런타임 시 오류가 발생 합니다.
6. 빌드하고 hello 응용 프로그램을 실행 합니다. Tooyour 계정에 로그인 한 후에 hello 응용 프로그램을 중지할 수 있습니다.
7. Toohello 반환 **서버 탐색기** hello에 hello 값을 살펴보고 및 **IssuingAuthorityKeys** 및 **테 넌 트** 테이블입니다. 이러한가 되어 자동으로 다시 채워집니다 hello hello 페더레이션 메타 데이터 문서에서 적절 한 정보를 확인할 수 있습니다.

### <a name="vs2013"></a>리소스를 보호하며 Visual Studio 2013을 사용하여 만든 웹 API
Hello Web API 템플릿을 사용 하 여 Visual Studio 2013에서 web API 응용 프로그램을 만든 경우 다음 선택한 **조직 계정** hello에서 **인증 변경** 메뉴 하면 이미 있는 hello 응용 프로그램에서 필수 논리가 있습니다.

인증을 수동으로 구성한 경우 아래 지침을 hello toolearn 어떻게 tooconfigure 웹 API tooautomatically 키 정보를 업데이트 합니다.

hello 다음 코드 조각은 방법을 보여 주는 tooget hello 페더레이션 메타 데이터 문서에서 최신 키 hello hello를 사용 하 여 [JWT 토큰 처리기](https://msdn.microsoft.com/library/dn205065.aspx) toovalidate hello 토큰입니다. hello 코드 조각에서는 데이터베이스, 구성 파일 또는 다른 위치에서 든 관계 없이 Azure AD의 자체 캐싱 메커니즘 이후 지속 hello 키 toovalidate에 대 한 토큰을 사용 하 여 가정 합니다.

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IdentityModel.Tokens;
using System.Configuration;
using System.Security.Cryptography.X509Certificates;
using System.Xml;
using System.IdentityModel.Metadata;
using System.ServiceModel.Security;
using System.Threading;

namespace JWTValidation
{
    public class JWTValidator
    {
        private string MetadataAddress = "[Your Federation Metadata document address goes here]";

        // Validates hello JWT Token that's part of hello Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in hello Azure Classic Portal]",
                ValidIssuer = "[hello issuer for hello token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache hello signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from hello specified metadata document.
        public List<X509SecurityToken> GetSigningCertificates(string metadataAddress)
        {
            List<X509SecurityToken> tokens = new List<X509SecurityToken>();

            if (metadataAddress == null)
            {
                throw new ArgumentNullException(metadataAddress);
            }

            using (XmlReader metadataReader = XmlReader.Create(metadataAddress))
            {
                MetadataSerializer serializer = new MetadataSerializer()
                {
                    // Do not disable for production code
                    CertificateValidationMode = X509CertificateValidationMode.None
                };

                EntityDescriptor metadata = serializer.ReadMetadata(metadataReader) as EntityDescriptor;

                if (metadata != null)
                {
                    SecurityTokenServiceDescriptor stsd = metadata.RoleDescriptors.OfType<SecurityTokenServiceDescriptor>().First();

                    if (stsd != null)
                    {
                        IEnumerable<X509RawDataKeyIdentifierClause> x509DataClauses = stsd.Keys.Where(key => key.KeyInfo != null && (key.Use == KeyType.Signing || key.Use == KeyType.Unspecified)).
                                                             Select(key => key.KeyInfo.OfType<X509RawDataKeyIdentifierClause>().First());

                        tokens.AddRange(x509DataClauses.Select(token => new X509SecurityToken(new X509Certificate2(token.GetX509RawData()))));
                    }
                    else
                    {
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in hello metadata");
                    }
                }
                else
                {
                    throw new Exception("Invalid Federation Metadata document");
                }
            }
            return tokens;
        }
    }
}
```

### <a name="vs2012"></a>리소스를 보호하며 Visual Studio 2012를 사용하여 만든 웹 응용 프로그램
Visual Studio 2012에서 응용 프로그램을 빌드한 경우 아마도 사용한 Identity hello 및 액세스 도구 tooconfigure 응용 프로그램. Hello를 사용 하는 것 역시 [유효성 검사 발급자 이름 레지스트리 VINR ()](https://msdn.microsoft.com/library/dn205067.aspx)합니다. hello VINR은 신뢰할 수 있는 id 공급자 (Azure AD)에 대 한 정보를 유지 관리 하 고 해당에서 발급 한 toovalidate 토큰을 사용 하는 hello 키. hello VINR을 사용 하면 쉽게 tooautomatically 업데이트 hello 키 정보 hello 최신 페더레이션 메타 데이터와 관련 된 문서 검사 hello 구성이 최신 hello로 만료 된 경우 디렉터리에 다운로드 하 여 Web.config 파일에 저장 합니다. 문서 및 hello 응용 프로그램 toouse hello 새 키 업데이트 필요에 따라 합니다.

Hello 코드 샘플 또는 연습 문서 Microsoft에서 제공 하는 중 하나를 사용 하 여 응용 프로그램을 만든 경우 hello 키 롤오버 논리가 이미 프로젝트에 포함 됩니다. 아래 hello 코드 프로젝트에 이미 존재 한다는 것을 확인할 수 있습니다. 응용 프로그램에 아직 없는 경우이 논리를 하 고 올바르게 작동 tooverify tooadd 아래 hello 단계를 수행 합니다.

1. **솔루션 탐색기**, 참조 toohello 추가 **System.IdentityModel** hello 적절 한 프로젝트에 대 한 어셈블리입니다.
2. 열기 hello **Global.asax.cs** 파일을 hello 다음 추가 지시문을 사용 하 여:
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. 다음 메서드 toohello hello 추가 **Global.asax.cs** 파일:
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. Hello 호출 **refreshvalidationsettings ()** hello에 대 한 메서드 **application_start ()** 메서드에서 **Global.asax.cs** 표시 된 것 처럼:
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

다음이 단계를 따른 후 응용 프로그램의 Web.config hello hello 최신 키를 포함 하 여 hello 페더레이션 메타 데이터 문서에서 최신 정보로 업데이트 됩니다. 이 업데이트는 IIS;에서 응용 프로그램 풀 재활용 될 때마다 발생 합니다. 기본적으로 29 시간 마다 IIS toorecycle 응용 프로그램 설정 됩니다.

Hello 키 롤오버 논리가 작동 tooverify 아래 hello 단계를 수행 합니다.

1. 응용 프로그램 열기 hello 위의 hello 코드를 사용 하 고 있는지 확인 한 후 **Web.config** toohello 이동한 다음 파일  **<issuerNameRegistry>**  블록에서 구체적으로 다음 몇 줄만 작성 hello:
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. Hello에  **<add thumbprint=””>**  설정, 다른 모든 문자를 대체 하 여 hello 지문 값을 변경 합니다. Hello 저장 **Web.config** 파일입니다.
3. Hello 응용 프로그램을 빌드하고 실행 합니다. Hello 로그인 프로세스를 완료할 수 응용 프로그램 디렉터리의 페더레이션 메타 데이터 문서에서 hello 필요한 정보를 다운로드 하 여 hello 키를 정상적으로 업데이트 됩니다. 로그인 하는 데 문제가 있는 경우 hello를 참조 하 여 응용 프로그램의 hello 변경 올바른지 확인 [추가 로그온 tooYour 웹 응용 프로그램 사용 하 여 Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) 항목 또는 다운로드 한 후 조사 아래의 코드 예제는 hello: [ Azure Active Directory 용 다중 테 넌 트 클라우드 응용 프로그램](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b)합니다.

### <a name="vs2010"></a>리소스를 보호하며 Visual Studio 2008 또는 2010 및 .NET 3.5용 WIF(Windows Identity Foundation) v1.0을 사용하여 만든 웹 응용 프로그램
WIF v 1.0에서 응용 프로그램을 작성 하는 경우 디자인 하는 메커니즘이 제공된 tooautomatically 창 응용 프로그램의 구성 toouse 새 키.

* *가장 쉬운 방법은* hello hello 최신 메타 데이터 문서를 검색 하 고 구성을 업데이트할 수 있는 WIF SDK에에서 포함 된 hello FedUtil 도구를 사용 합니다.
* Hello hello System 네임 스페이스에는 WIF의 최신 버전을 포함 하 여 응용 프로그램 too.NET 4.5를 업데이트 합니다. Hello를 사용 하 여 있습니다 [유효성 검사 발급자 이름 레지스트리 VINR ()](https://msdn.microsoft.com/library/dn205067.aspx) hello 응용 프로그램의 구성 tooperform 자동 업데이트 합니다.
* 이 지침 문서 hello 끝나기 전에 hello 지침에 따라 수동 롤오버를 수행 합니다.

Toouse hello FedUtil tooupdate 구성 지침:

1. Hello WIF v1.0 SDK가 Visual Studio 2008 또는 2010 용 개발 컴퓨터에 설치 되어 있는지 확인 합니다. 아직 설치되어 있지 않은 경우 [여기에서 다운로드](https://www.microsoft.com/en-us/download/details.aspx?id=4451) 할 수 있습니다.
2. Visual Studio에서 hello 솔루션을 열고 다음 hello 응용 프로그램 프로젝트를 마우스 오른쪽 단추로 클릭 및 선택 **페더레이션 메타 데이터 업데이트**합니다. 이 옵션을 사용할 수 없는 경우 FedUtil 및/또는 hello WIF v1.0 SDK 설치 되지 않았습니다.
3. Hello 프롬프트에서 선택 **업데이트** toobegin 페더레이션 메타 데이터를 업데이트 합니다. Hello 응용 프로그램이 호스팅된 곳 액세스 toohello 서버 환경에 있으면 FedUtil의 필요에 따라 사용할 수 있습니다 [자동 메타 데이터 업데이트 스케줄러](https://msdn.microsoft.com/library/ee517272.aspx)합니다.
4. 클릭 **마침** toocomplete hello 업데이트 프로세스입니다.

### <a name="other"></a>웹 응용 프로그램/리소스를 보호 하는 Api를 사용 하 여 다른 라이브러리 또는 수동으로 구현 하는 hello의 지원 되는 프로토콜
Tooreview hello 라이브러리 해야 또는 hello 또는 hello OpenID Connect 검색 문서에서 키 hello 프로그램 구현 tooensure를 검색 하는 일부 다른 라이브러리를 사용 하는 하거나 수동으로 hello 지원 프로토콜의 구현 된 경우 페더레이션 메타 데이터 문서입니다. 이 한 가지 방법은 toocheck toodo tooeither hello OpenID 검색 문서 또는 hello 페더레이션 메타 데이터 문서는 모든 호출에 대 한 코드나 hello 라이브러리 코드의 검색입니다.

Hello 키와 업데이트를 적절 하 게 하 여 수행할 것 hello 지침 문서가이 끝나기 전에 hello 지침에 따라 수동 롤오버를 검색할 어딘가에 저장 되는 키 또는 하드 코딩 된 응용 프로그램을 수동으로 실행할 수 있습니다. **좋습니다 응용 프로그램 toosupport 자동 롤오버를 향상 시키는** hello를 사용 하 여 Azure AD 롤오버 운율 늘어나거나가이 문서 tooavoid 이후 중단 오버 헤드의 개요에 도달한는 응급 대역의 롤오버입니다.

## <a name="how-tootest-your-application-toodetermine-if-it-will-be-affected"></a>어떻게 tootest 프로그램 응용 프로그램 toodetermine 영향을 받게 됩니다 하는 경우
응용 프로그램 hello 스크립트를 다운로드 하 고 hello 지침에 자동 키 롤오버를 지원 하는지 여부를 확인할 수 있습니다 [이 GitHub 리포지토리 합니다.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)

## <a name="how-tooperform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a>어떻게 응용 프로그램 자동 롤오버를 지원 하지 않는 경우 수동 롤오버 tooperform
응용 프로그램은 경우 **하지** 자동 롤오버 지원, 그에 따라 tooestablish 프로세스를 주기적으로 모니터 Azure AD의 서명 키를 수동 롤오버를 수행 해야 합니다. [이 GitHub 리포지토리](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) 스크립트 및 방법에 대 한 지침이 포함 되어 toodo이 있습니다.

