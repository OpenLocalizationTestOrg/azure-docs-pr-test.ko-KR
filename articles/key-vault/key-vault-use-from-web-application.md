---
title: "웹 응용 프로그램에서 Azure 주요 자격 증명 모음 aaaUse | Microsoft Docs"
description: "이 자습서 toohelp 배웁니다, 어떻게 toouse Azure 키 자격 증명 모음에 있는 웹 응용 프로그램을 사용 합니다."
services: key-vault
documentationcenter: 
author: adhurwit
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 9b7d065e-1979-4397-8298-eeba3aec4792
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: adhurwit
ms.openlocfilehash: d5e2299e60b379c4e234d5cd6be03411c5a5c958
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-key-vault-from-a-web-application"></a>웹 응용 프로그램에서 Azure 주요 자격 증명 모음 사용
## <a name="introduction"></a>소개
이 자습서에 어떻게 toouse Azure 키 자격 증명 모음에 있는 웹 응용 프로그램을 Azure에 알아봅니다 toohelp를 사용 합니다. 웹 응용 프로그램에서 사용할 수 있도록 Azure 키 자격 증명 모음에서 암호에 액세스 하는 hello 과정을 안내 합니다.

**예상 시간 toocomplete:** 15 분

Azure 키 자격 증명 모음에 대한 개요는 [Azure 키 자격 증명 모음이란?](key-vault-whatis.md)

## <a name="prerequisites"></a>필수 조건
toocomplete이이 자습서에서는 다음 hello 있어야 합니다.

* Azure 키 자격 증명 모음에 사용 되는 URI tooa 암호
* 클라이언트 ID 및 클라이언트 암호는 웹 응용 프로그램에 대 한 액세스 tooyour 주요 자격 증명 모음에 있는 Azure Active Directory에 등록
* 웹 응용 프로그램. 웹 앱으로 Azure에 배포 된 ASP.NET MVC 응용 프로그램에 대 한 hello 단계를 보여 줄 것입니다.

> [!NOTE]
> 에 나열 된 hello 단계를 완료 해야 [Azure 키 자격 증명 모음 시작](key-vault-get-started.md) 이 자습서를 마쳤으므로 hello URI tooa 암호 및 hello 클라이언트 ID와 클라이언트 암호는 웹 응용 프로그램에 대 한 합니다.
> 
> 

hello 키 자격 증명 모음에 액세스 하는 hello 웹 응용 프로그램에는 Azure Active Directory에 등록 되 고 액세스 tooyour 주요 자격 증명 모음 부여 되었는지 여부를 지정 하는 하나 hello입니다. 이 정보가 hello 대/소문자를 tooRegister hello 시작 자습서의 응용 프로그램을 다시 이동 하 고 나열 된 hello 단계를 반복 합니다.

이 자습서는 Azure에서 웹 응용 프로그램을 만드는 hello 기본 사항을 이해 하는 웹 개발자를 위해 설계 되었습니다. Azure 웹앱에 대한 자세한 내용은 [웹앱 개요](../app-service-web/app-service-web-overview.md)를 참조하세요.

## <a id="packages"></a>NuGet 패키지 추가
웹 응용 프로그램 toohave 설치에 필요한 두 개의 패키지가 있습니다.

* Active Directory 인증 라이브러리 - Azure Active Directory를 조작하고 사용자 ID를 관리하기 위한 메서드를 포함합니다.
* Azure 주요 자격 증명 모음 라이브러리 - Azure 주요 자격 증명 모음을 조작하기 위한 메서드를 포함합니다.

이러한 패키지 중 둘 다 사용 하 여 설치할 수 hello Install-package 명령을 사용 하 여 패키지 관리자 콘솔 hello 합니다.

    // this is currently hello latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <a id="webconfig"></a>Web.Config 수정
세 가지 응용 프로그램 설정을 toobe 추가 toohello web.config 파일을 다음과 같이 필요 합니다.

    <!-- ClientId and ClientSecret refer toohello web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is hello URI for hello secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


않으려는 toohost Azure 웹 앱으로 응용 프로그램, hello 실제 ClientId, 클라이언트 암호 및 암호 URI 값 toohello web.config을 추가 해야 합니다. Azure 포털의 보안 수준 높이기 위해 hello에 hello 실제 값으로 추가 하기 때문에 이러한 dummy 값 둡니다.

## <a id="gettoken"></a>메서드 tooGet 액세스 토큰을 추가 합니다.
순서 toouse hello 키 자격 증명 모음 API에에서 액세스 토큰이 필요 합니다. 키 자격 증명 모음 API toohello 해야만 toosupply 호출을 처리 하는 키 자격 증명 모음 클라이언트 hello 사용 하 여 hello 액세스 토큰을 가져오는 함수는 합니다.  

다음은 hello 코드 tooget Azure Active Directory에서 액세스 토큰입니다. 이 코드는 응용 프로그램의 아무 곳에나 배치할 수 있습니다. 마음에 tooadd는 유틸리티 또는 EncryptionHelper 클래스.  

    //add these using statements
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Threading.Tasks;
    using System.Web.Configuration;

    //this is an optional property toohold hello secret after it is retrieved
    public static string EncryptSecret { get; set; }

    //hello method that will be provided toohello KeyVaultClient
    public static async Task<string> GetToken(string authority, string resource, string scope)
    {
        var authContext = new AuthenticationContext(authority);
        ClientCredential clientCred = new ClientCredential(WebConfigurationManager.AppSettings["ClientId"],
                    WebConfigurationManager.AppSettings["ClientSecret"]);
        AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

        if (result == null)
            throw new InvalidOperationException("Failed tooobtain hello JWT token");

        return result.AccessToken;
    }

> [!NOTE]
> 클라이언트 ID와 클라이언트 암호를 사용 하 여 hello 가장 쉬운 방법은 tooauthenticate Azure AD 응용 프로그램입니다. 웹 응용 프로그램에서 클라이언트 ID 및 클라이언트 암호를 사용하여 의무를 분리하고 키 관리를 보다 세밀하게 제어할 수 있습니다. 하지만 일부에 대 한 구성 설정에서 tooprotect 되도록 hello 비밀 배치로으로 것은 위험할 수 있는 구성 설정에서 hello 클라이언트 암호를 배치에 의존지 않습니다. 어떻게 toouse 클라이언트 ID 및 인증서 클라이언트 ID와 클라이언트 암호가 tooauthenticate 대신 hello Azure AD 응용 프로그램에 대 한 내용은 아래를 참조 하십시오.
> 
> 

## <a id="appstart"></a>Hello 보안 응용 프로그램 시작을 검색 합니다.
이제 toocall hello 키 자격 증명 모음 API를 코드 및 hello 암호를 검색할 필요 합니다. hello 다음 코드 전환할 수 있습니다. 원격으로 toouse 필요 하기 전에 호출 될 것입니다. 시작 시에 한 번 실행 하 고는 hello 비밀 hello 응용 프로그램에 사용할 수 있도록 hello Global.asax에에서 hello 응용 프로그램 시작 이벤트에서이 코드를 배치 했습니다.

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class toohold hello secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <a id="portalsettings"></a>Azure 포털 (선택 사항) hello에 응용 프로그램 설정을 추가합니다
Azure 웹 앱이 있는 경우 hello Azure 포털에서에서 이제 hello AppSettings hello에 대 한 실제 값을 추가할 수 있습니다. 이 작업을 수행 하 여 hello 실제 값 hello web.config에 위치 하지 않습니다 있지만 hello 별도 액세스 제어 기능이 제공 되는 포털을 통해 보호 됩니다. Web.config 파일에 입력 한 hello 값에 대 한 이러한 값이 대체 됩니다. Hello 이름은 동일 hello는 있는지 확인 합니다.

![Azure 포털에 표시되는 응용 프로그램 설정][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a>클라이언트 암호 대신 인증서로 인증
또 다른 방법은 tooauthenticate Azure AD 응용 프로그램 클라이언트 ID와 클라이언트 암호 대신 클라이언트 ID 및 인증서를 사용 하는 것입니다. 다음 단계는 Azure 웹 앱에 인증서가 toouse를 hello 됩니다.

1. 인증서 얻기 또는 만들기
2. Hello 인증서는 Azure AD 응용 프로그램에 연결
3. 코드 tooyour 웹 앱 toouse hello 인증서 추가
4. 인증서 tooyour 웹 응용 프로그램 추가

**인증서 얻기 또는 만들기** 학습을 위한 목적으로 테스트 인증서를 만듭니다. 다음은 몇 가지 명령 사용할 수 있는 개발자 명령 프롬프트 toocreate에 인증서입니다. 디렉터리 toowhere 만든 hello 인증서 파일을 변경 합니다.  또한 시작 및 끝 날짜 hello 인증서의 hello에 대 한 사용 하 여 hello 현재 날짜와 1 년입니다.

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

Hello 종료 날짜 및 hello.pfx에 대 한 hello 암호를 기록 (이 예제의: 07/31/2016 및 test123). 아래에서 필요합니다.

테스트 인증서 만들기에 대한 자세한 내용은 [방법: 사용자 고유의 테스트 인증서 만들기](https://msdn.microsoft.com/library/ff699202.aspx)

**Azure AD 응용 프로그램으로 연결 hello 인증서** tooassociate 필요한 인증서를가지고 사용 하 여 Azure AD 응용 프로그램입니다. 현재는 Azure 포털 hello이이 워크플로; 지원 하지 않습니다. PowerShell을 통해이 완료할 수 있습니다. Hello 명령을 tooassoicate hello 인증서 hello Azure AD 응용 프로그램으로 다음을 실행 합니다.

    $x509 = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $x509.Import("C:\data\KVWebApp.cer")
    $credValue = [System.Convert]::ToBase64String($x509.GetRawCertData())

    # If you used different dates for makecert then adjust these values
    $now = [System.DateTime]::Now
    $yearfromnow = $now.AddYears(1)

    $adapp = New-AzureRmADApplication -DisplayName "KVWebApp" -HomePage "http://kvwebapp" -IdentifierUris "http://kvwebapp" -CertValue $credValue -StartDate $now -EndDate $yearfromnow

    $sp = New-AzureRmADServicePrincipal -ApplicationId $adapp.ApplicationId

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'contosokv' -ServicePrincipalName $sp.ServicePrincipalName -PermissionsToSecrets all -ResourceGroupName 'contosorg'

    # get hello thumbprint toouse in your app settings
    $x509.Thumbprint

이러한 명령은 실행 한 후에 Azure AD에서 hello 응용 프로그램을 볼 수 있습니다. 를 검색할 때 "회사가 보유 한 응용 프로그램" 선택 "응용 프로그램 사용" 대신에 확인 hello 검색 대화 상자.

Azure AD 응용 프로그램 개체 및 ServicePrincipal 개체에 대해 자세히 toolearn 참조 [응용 프로그램 개체 및 서비스 사용자 개체](../active-directory/active-directory-application-objects.md)

**추가 코드 tooyour 웹 앱 toouse hello 인증서** 이제 코드 tooyour 웹 앱 tooaccess cert hello 및 인증을 위해 사용 하 여 추가 합니다.

먼저 코드 tooaccess hello 인증서가 있습니다.

    public static class CertificateHelper
    {
        public static X509Certificate2 FindCertificateByThumbprint(string findValue)
        {
            X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
            try
            {
                store.Open(OpenFlags.ReadOnly);
                X509Certificate2Collection col = store.Certificates.Find(X509FindType.FindByThumbprint,
                    findValue, false); // Don't validate certs, since hello test root isn't installed.
                if (col == null || col.Count == 0)
                    return null;
                return col[0];
            }
            finally
            {
                store.Close();
            }
        }
    }


해당 hello StoreLocation은 LocalMachine 대신 CurrentUser note 합니다. 테스트 인증서를 사용 중 이므로 'false' toohello 제공 하는 것을 Find 메서드.

다음은 코드를 CertificateHelper hello를 사용 하며 인증에 필요한 ClientAssertionCertificate를 만듭니다.

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


다음은 hello 새 코드 tooget hello 액세스 토큰입니다. 위의 hello GetToken 메서드를 대체 합니다. 편의를 위해 다른 이름을 부여했습니다.

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

사용 편의를 위해 이 모든 코드를 웹앱 프로젝트의 Utils 클래스에 넣어 두었습니다.

hello 마지막 코드 변경이 hello Application_Start 메서드가입니다. 먼저 toocall hello GetCert() 메서드 tooload hello ClientAssertionCertificate 해야 합니다. 한 다음 새 KeyVaultClient를 만들 때 제공 하는 hello 콜백 메서드를 변경 했습니다. 위에서 몇 hello 코드를 대체이 note 합니다.

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


**Hello Azure 포털을 통해 인증서 tooyour 웹 응용 프로그램 추가** 인증서 tooyour 웹 응용 프로그램을 추가 하는 것은 간단한 2 단계 프로세스입니다. 먼저, Azure 포털 toohello 이동 하 고 tooyour 웹 응용 프로그램을 이동 합니다. 웹 앱에 대 한 hello 설정 블레이드에서 "사용자 지정 도메인 및 SSL"에 대 한 hello 항목을 클릭 합니다. Hello에 하면 블레이드 컴퓨터 이름은 수 tooupload hello KVWebApp.pfx 위에서 만든 인증서를 반드시 hello pfx에 대 한 hello 암호를 기억해 야 합니다.

![Hello Azure 포털에서에서 인증서 tooa 웹 응용 프로그램 추가][2]

hello toodo를 필요한 것은 응용 프로그램 설정 tooyour hello 이름 웹 사이트에 웹 앱 tooadd\_부하\_인증서 및 값이 * 합니다. 이렇게 하면 모든 인증서가 로드됩니다. 하려는 경우이 단계는 tooload만 hello 인증서를 업로드 한 경우 해당 지문 쉼표로 구분 된 목록에 입력할 수 있습니다.

추가 인증서 tooa 웹 앱에 대 한 더 toolearn 참조 [Azure 웹 사이트 응용 프로그램에 대 한 인증서를 사용 하 여](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)

**암호로 인증서 tooKey 자격 증명 모음을 추가** 사용자 인증서 toohello 웹 응용 프로그램 서비스를 직접 업로드 하는 대신는 암호로 키 자격 증명 모음에 저장 한 위치에서 배포할 수 있습니다. 이 hello 다음 블로그 게시물에에서 설명 된 2 단계 프로세스 [주요 자격 증명 모음을 통해 Azure 웹 앱 인증서 배포](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)

## <a id="next"></a>다음 단계
프로그래밍 참조는 [Azure 주요 자격 증명 모음 C# 클라이언트 API 참조](https://msdn.microsoft.com/library/azure/dn903628.aspx)를 참조하세요.

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
