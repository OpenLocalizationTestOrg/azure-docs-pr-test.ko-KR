---
title: "Azure AD 인증.NET을 사용 하 여 Azure 미디어 서비스 API tooaccess aaaUse | Microsoft Docs"
description: "이 항목에서는 Azure 미디어 서비스 하는 Azure Active Directory (Azure AD) 인증 tooaccess toouse 방법을 보여 줍니다..net AMS () API입니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 2f750e460d9e476ad92e96adeac6500cb692cd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-azure-media-services-api-with-net"></a>Azure AD 인증 tooaccess Azure 미디어 서비스 API를 사용 하 여.net

windowsazure.mediaservices 4.0.0.4부터는 Azure Media Services에서 Azure AD(Azure Active Directory) 기반 인증을 지원합니다. 이 항목에서는 Azure AD 인증 tooaccess Microsoft.net Azure 미디어 서비스 API toouse 합니다.

## <a name="prerequisites"></a>필수 조건

- Azure 계정. 자세한 내용은 [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요. 
- Media Services 계정. 자세한 내용은 참조 [hello Azure 포털을 사용 하 여 Azure 미디어 서비스 계정 만들기](media-services-portal-create-account.md)합니다.
- 최신 hello [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) 패키지 합니다.
- Hello 항목 익숙하다고 [AAD 인증 개요를 사용 하 여 Azure 미디어 서비스 API에 액세스](media-services-use-aad-auth-to-access-ams-api.md)합니다. 

Azure Media Services와 함께 Azure AD 인증을 사용할 때 다음 두 가지 방법 중 하나로 인증할 수 있습니다.

- **사용자 인증** hello 앱 toointeract Azure 미디어 서비스 리소스와 함께 사용 하는 사람을 인증 합니다. 먼저 hello 대화형 응용 프로그램에는 hello 사용자에 게 자격 라는 메시지 해야 합니다. 예에는 라이브 스트리밍 또는 권한이 있는 사용자 toomonitor 인코딩 작업에서 사용 하는 관리 콘솔 앱입니다. 
- **서비스 주체 인증**은 서비스를 인증합니다. 이 인증 방법을 일반적으로 사용하는 응용 프로그램은 디먼 서비스, 중간 계층 서비스 또는 예약된 작업(예: 웹앱, 함수 앱, 논리 앱, API 또는 마이크로 서비스)을 실행하는 앱입니다.

>[!IMPORTANT]
>현재 Azure Media Services는 Azure Access Control Service 인증 모델을 지원합니다. 그러나 액세스 제어 권한 부여는 toobe 2018 년 6 월 1에서 더 이상 사용 되지 것입니다. Tooan Azure Active Directory 인증 모델을 최대한 빨리 마이그레이션하는 것이 좋습니다.

## <a name="get-an-azure-ad-access-token"></a>Azure AD 액세스 토큰 가져오기

Azure AD 인증 tooconnect toohello Azure 미디어 서비스 API를 hello 클라이언트 응용 프로그램 toorequest Azure AD 액세스 토큰을 필요합니다. Hello 미디어 서비스.NET SDK tooacquire는 Azure AD 액세스 토큰은 래핑된 하 고 hello를 간소화 하는 방법에 대 한 hello 정보의 많은 클라이언트를 사용 하는 경우 [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) 및 [AzureAdTokenCredentials ](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) 클래스입니다. 

예를 들어 않아도 tooprovide hello Azure AD 인증 기관, URI, 미디어 서비스 리소스 또는 네이티브 Azure AD 응용 프로그램 세부 정보입니다. 이들은 hello Azure AD 액세스 토큰 공급자 클래스에서 이미 구성 되어 있는 잘 알려진 값입니다. 

Azure 미디어 서비스.NET SDK를 사용 하지 않는 경우 hello를 사용 하는 것이 좋습니다 [Azure AD 인증 라이브러리](../active-directory/develop/active-directory-authentication-libraries.md)합니다. Azure AD 인증 라이브러리와 toouse 해야 하는 hello 매개 변수에 대 한 tooget 값 참조 [hello Azure 포털 tooaccess Azure AD 인증 설정을 사용 하 여](media-services-portal-get-started-with-aad.md)합니다.

교체 hello의 기본 구현은 hello hello 옵션도 제공 **AzureAdTokenProvider** 사용자 구현으로 합니다.

## <a name="install-and-configure-azure-media-services-net-sdk"></a>Azure Media Services .NET SDK 설치 및 구성

>[!NOTE] 
>미디어 서비스.NET SDK hello로 toouse Azure AD 인증을 해야 toohave hello 최신 [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) 패키지 합니다. 또한 참조 toohello 추가 **Microsoft.IdentityModel.Clients.ActiveDirectory** 어셈블리입니다. 기존 앱을 사용 하는 경우 포함 hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** 어셈블리입니다. 

1. Visual Studio를 사용하여 새 C# 콘솔 응용 프로그램을 만듭니다.
2. 사용 하 여 hello [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet 패키지 tooinstall **Azure 미디어 서비스.NET SDK**합니다. 

    NuGet을 사용 하 여 tooadd 참조 수행할 단계를 수행 하는 hello:에서 **솔루션 탐색기**를 hello 프로젝트 이름을 마우스 오른쪽 단추로 클릭 한 다음 선택 **NuGet 패키지 관리**합니다. 그런 다음 **windowsazure.mediaservices**를 검색하고 **설치**를 선택합니다.
    
    또는

    실행 hello 다음에 명령을 **패키지 관리자 콘솔** Visual Studio에서.

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. 추가 **를 사용 하 여** tooyour 소스 코드입니다.

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a>사용자 인증 사용

tooconnect toohello hello 사용자 인증 옵션과 함께 Azure 미디어 서비스 API, hello 클라이언트 응용 프로그램에는 Azure AD 토큰을 사용 하 여 매개 변수 뒤 hello toorequest 항목이 필요 합니다.  

- Azure AD 테넌트 끝점. hello Azure 포털에서에서 hello 테 넌 트 정보를 검색할 수 있습니다. Hello 로그인 한 사용자 hello 오른쪽 위 모서리에 올려 놓습니다.
- Media Services 리소스 URI.
- Media Services(원시) 응용 프로그램 클라이언트 ID. 
- Media Services(원시) 응용 프로그램 리디렉션 URI. 

이러한 매개 변수에 대 한 hello 값에서 찾을 수 있습니다 **AzureEnvironments.AzureCloudEnvironment**합니다. hello **AzureEnvironments.AzureCloudEnvironment** 상수이 함수는 hello.NET SDK tooget에서 공용 Azure 데이터 센터에 대 한 hello 오른쪽 환경 변수 설정 합니다. 

공용 데이터 센터 전용 hello에에서 미디어 서비스에 액세스 하기 위한 미리 정의 된 환경 설정을 포함 합니다. 독립 또는 정부 클라우드 지역의 경우 **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment** 또는 **AzureGermanCloudEnvironment**를 각각 사용할 수 있습니다.

다음 코드 예제는 hello 토큰을 만듭니다.
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
toostart 미디어 서비스를 대상으로 프로그래밍 해야 toocreate는 **CloudMediaContext** hello 서버 컨텍스트를 나타내는 인스턴스입니다. hello **CloudMediaContext** 작업, 자산, 파일, 액세스 정책 및 로케이터를 포함 하 여 참조 tooimportant 컬렉션이 포함 되어 있습니다. 

또한 toopass hello 해야 **리소스 미디어 REST 서비스에 대 한 URI** toohello **CloudMediaContext** 생성자입니다. tooget hello 리소스 URI 미디어 REST 서비스에서 toohello Azure 포털에에서 로그인 사용자의 Azure 미디어 서비스 계정 선택에 대 한 선택 **API 액세스**를 선택한 후 **tooAzure 미디어 서비스 사용자와 연결 인증**합니다. 

hello 다음 코드 예제에서는 한 **CloudMediaContext** 인스턴스:

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

다음 예제는 hello toocreate Azure AD 토큰 및 hello 컨텍스트가 hello 하는 방법을 보여 줍니다.

    namespace AADAuthSample
    {
        class Program
        {
            static void Main(string[] args)
            {
                // Specify your Azure AD tenant domain, for example "microsoft.onmicrosoft.com".
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR AAD TENANT DOMAIN HERE}", AzureEnvironments.AzureCloudEnvironment);
    
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
            }
    
        }
    }

>[!NOTE]
>라고 표시 하는 예외를 발생 하는 경우 "hello 원격 서버에 오류가 반환 되었습니다: (401) 권한 없음" hello 참조 [액세스 제어](media-services-use-aad-auth-to-access-ams-api.md#access-control) Azure 미디어 서비스 API에 액세스의 Azure AD 인증 개요 섹션.

## <a name="use-service-principal-authentication"></a>서비스 주체 인증 사용
    
tooconnect toohello Azure 미디어 서비스 API hello 서비스 보안 주체 옵션으로, 중간 계층 응용 프로그램 (웹 API 또는 웹 응용 프로그램) 매개 변수 뒤 hello로 toorequests는 Azure AD 토큰 항목이 필요 합니다.  

- Azure AD 테넌트 끝점. hello Azure 포털에서에서 hello 테 넌 트 정보를 검색할 수 있습니다. Hello 로그인 한 사용자 hello 오른쪽 위 모서리에 올려 놓습니다.
- Media Services 리소스 URI.
- Azure AD 응용 프로그램 값: hello **클라이언트 ID** 및 **클라이언트 암호**합니다.

hello에 대 한 값을 hello **클라이언트 ID** 및 **클라이언트 암호** hello Azure 포털에서에서 매개 변수를 찾을 수 있습니다. 자세한 내용은 참조 [Azure 포털 hello 사용 하 여 Azure AD 인증 시작](media-services-portal-get-started-with-aad.md)합니다.

hello 다음 코드 예제에서는 토큰을 사용 하 여 만듭니다 hello **AzureAdTokenCredentials** 사용 하는 생성자 **AzureAdClientSymmetricKey** 매개 변수로: 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

Hello를 지정할 수도 있습니다 **AzureAdTokenCredentials** 사용 하는 생성자 **AzureAdClientCertificate** 매개 변수로 합니다. 

방법에 대 한 지침은 toocreate 참조, Azure AD에서 사용할 수 있는 형태로 인증서를 구성 하 고 [tooAzure AD 인증서-수동 구성 단계를 사용 하 여 디먼 앱에 인증](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md)합니다.

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

toostart 미디어 서비스를 대상으로 프로그래밍 해야 toocreate는 **CloudMediaContext** hello 서버 컨텍스트를 나타내는 인스턴스입니다. 또한 toopass hello 해야 **리소스 미디어 REST 서비스에 대 한 URI** toohello **CloudMediaContext** 생성자입니다. Hello를 얻을 수 **리소스 미디어 REST 서비스에 대 한 URI** hello도 Azure 포털의 값입니다.

hello 다음 코드 예제에서는 한 **CloudMediaContext** 인스턴스:

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
다음 예제는 hello toocreate Azure AD 토큰 및 hello 컨텍스트가 hello 하는 방법을 보여 줍니다.

    namespace AADAuthSample
    {
    
        class Program
        {
            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                            new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                            AzureEnvironments.AzureCloudEnvironment);
            
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".      
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
    
                Console.ReadLine();
            }
    
        }
    }

## <a name="next-steps"></a>다음 단계

시작 [tooyour 계정에 파일 업로드](media-services-dotnet-upload-files.md)합니다.
