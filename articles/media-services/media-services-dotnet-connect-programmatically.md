---
title: ".NET을 사용 하 여 aaaConnecting tooMedia 서비스 계정"
description: "이 항목에서 설명 방법을 tooconnect tooMedia 서비스 데.NET 합니다."
services: media-services
documentationcenter: 
author: juliako
manager: erikre
editor: 
ms.assetid: a8412a29-59dc-44a0-ace0-be79a97dab63
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: a23bd285f7cae17ae5831e1e50e73947afbb9a3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-toomedia-services-account-using-media-services-sdk-for-net"></a>TooMedia.NET 용 미디어 서비스 SDK를 사용 하 여 서비스 계정 연결
> [!div class="op_single_selector"]
> * [REST (영문)](media-services-rest-connect-programmatically.md)
> * [.NET](media-services-dotnet-connect-programmatically.md)
> 
> 

이 항목에서는 tooobtain 프로그래밍 방식으로 연결 tooMicrosoft Azure 미디어 서비스를 사용 하 여 프로그래밍할 때 Media Services SDK for.NET hello 하는 방법을 설명 합니다.

## <a name="connecting-toomedia-services"></a>TooMedia 서비스 연결
tooconnect tooMedia 프로그래밍 방식으로 서비스는 이전에 Azure 계정을 설정, 해당 계정에 미디어 서비스를 구성 하며.NET 용 hello Media Services SDK로 개발을 위한 Visual Studio 프로젝트를 설정 합니다. 자세한 내용은.NET 용 개발을 위한 설치 프로그램을 hello Media Services SDK로 참조 합니다.

Hello 미디어 서비스 계정 설정 프로세스의 hello 끝을 구입한 hello 다음과 같은 필수 연결 값입니다. 이러한 toomake 프로그래밍 방식으로 연결을 사용 하 여 tooMedia 서비스입니다.

* Media Services 계정 이름.
* Media Services 계정 키.

toofind 이들 값이 이동 toohello Azure 관리 포털 여 미디어 서비스 계정을 선택 하 고 hello 클릭 "**키 관리**" hello hello 포털 창 하단에서 아이콘입니다. Hello 아이콘 다음 tooeach 텍스트 상자 복사본 hello 값 toohello 시스템 클립보드에 여기를 클릭합니다.

## <a name="creating-a-cloudmediacontext-instance"></a>CloudMediaContext 인스턴스 만들기
toocreate 필요한 서비스를 미디어에 대 한 프로그래밍 toostart는 **CloudMediaContext** hello 서버 컨텍스트를 나타내는 인스턴스입니다. hello **CloudMediaContext** 작업, 자산, 파일, 액세스 정책 및 로케이터를 포함 하 여 참조 tooimportant 컬렉션이 포함 되어 있습니다.

> [!NOTE]
> hello **CloudMediaContext** 클래스는 스레드로부터 안전 하지 않습니다. 스레드마다 또는 작업 집합마다 새 CloudMediaContext를 만들어야 합니다.
> 
> 

CloudMediaContext에는 5개의 생성자 오버로드가 있습니다. 사용 하는 권장된 toouse 생성자는 **MediaServicesCredentials** 매개 변수로 합니다. 자세한 내용은 참조 hello **액세스 제어 서비스 토큰 다시 사용** 다음에 오는 합니다. 

hello 다음 예제에서는 public CloudMediaContext(MediaServicesCredentials credentials) 생성자 hello:

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a>액세스 제어 서비스 토큰 다시 사용
이 섹션에서는 MediaServicesCredentials 매개 변수로 사용 하는 CloudMediaContext 생성자를 사용 하 여 tooreuse 액세스 제어 서비스 토큰 하는 방법을 보여 줍니다.

[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (액세스 제어 서비스 또는 ACS 라고도 함)는 tootheir 웹 응용 프로그램 인증 및 권한 부여 사용자 toogain 액세스는 쉬운 방법을 제공 하는 클라우드 기반 서비스입니다. Microsoft Azure 미디어 서비스 액세스 제어 서비스 tooits 하지만 ACS 토큰이 필요한 OAuth 프로토콜 합니다. 미디어 서비스는 권한 부여 서버에서 hello ACS 토큰을 받습니다.

때문에 처리 하도록 hello 토큰 toonot hello Media Services SDK를 개발할 때 선택할 수 있습니다 SDK 코드 관리자 hello ç 있습니다. 그러나 줍니다 hello SDK hello ACS 토큰 리드 toounnecessary 토큰 요청을 관리 하는 완벽 하 게 합니다. 토큰 요청은 시간이 걸리며 hello 클라이언트와 서버 리소스를 사용 합니다. 또한 hello 속도가 너무 높은 경우 ACS 서버 hello hello 요청을 제한 합니다. hello 제한은 초당 요청 30, 참조 [ACS 서비스 제한](https://msdn.microsoft.com/library/gg185909.aspx) 내용을 확인 합니다.

Hello 미디어 서비스 SDK 버전 3.0.0.0 부터는 ACS 토큰 hello를 다시 사용할 수 있습니다. hello **CloudMediaContext** 사용 하는 생성자 **MediaServicesCredentials** 매개 변수로 여러 컨텍스트 간에 공유 hello ACS 토큰을 사용 하도록 설정 합니다. hello MediaServicesCredentials 클래스 hello 미디어 서비스 자격 증명을 캡슐화합니다. ACS 토큰을 사용할 수 있는 경우 해당 만료 시간이 알려진 새 MediaServicesCredentials 인스턴스 hello 토큰으로 만들고 CloudMediaContext의 toohello 생성자를 전달할 수 있습니다. 미디어 서비스 SDK를 자동으로 hello는 만료 될 때마다 토큰을 새로 고칩니다. 두 가지가 tooreuse ACS 토큰을 아래 hello 예제와 같이 합니다.

* Hello를 캐시 하면 **MediaServicesCredentials** (예: 정적 클래스 변수)에 메모리의 개체입니다. 그런 다음 캐시 된 hello 개체 toohello CloudMediaContext 생성자를 전달 합니다. MediaServicesCredentials 개체에 hello 여전히 유효한 경우 다시 사용할 수 있는 ACS 토큰을 포함 합니다. Hello 토큰이 유효 하지 않을 경우, hello로 새로 고쳐 hello 자격 증명을 사용 하 여 Media Services SDK toohello MediaServicesCredentials 생성자를 제공 합니다.
  
    해당 hello 참고 **MediaServicesCredentials** 개체 RefreshToken 라고 하는 hello 후 유효한 토큰을 가져옵니다. hello **CloudMediaContext** 호출 hello **RefreshToken** hello 생성자입니다. Toosave hello 토큰 값 tooan 외부 저장소를 계획 하는 경우 있는지 toocheck hello TokenExpiration 값 hello 토큰 데이터를 저장 하기 전에 유효한 지 여부를 확인 합니다. 유효하지 않으면 캐싱 전에 RefreshToken을 호출 합니다.
  
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use hello cached credentials toocreate a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* Hello AccessToken 문자열 및 hello TokenExpiration 값 캐시할 수 있습니다. hello 값에 사용 되는 toocreate hello 캐시 된 토큰 데이터로 새 MediaServicesCredentials 개체 수 나중에 있습니다.  이 hello 토큰 공유할 수 있는 안전 하 게 여러 프로세스 또는 컴퓨터 간에 시나리오에 특히 유용 합니다.
  
    hello 다음 코드 조각 호출 hello이 예에서 정의 되어 있지 않은 SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage 및 UpdateTokenDataInExternalStorageIfNeeded 메서드. 외부 저장소에서 이러한 메서드 toostore, 검색, 및 업데이트 토큰 데이터를 정의할 수 있습니다. 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from hello context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // hello SaveTokenDataToExternalStorage method should check 
        // whether hello TokenExpiration value is valid before saving hello token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    토큰 값 toocreate MediaServicesCredentials 저장 hello를 사용 합니다.

        var accessToken = "";
        var tokenExpiration = DateTime.UtcNow;

        // Retrieve saved token values.
        GetTokenDataFromExternalStorage(out accessToken, out tokenExpiration);

        // Create a new MediaServicesCredentials object using saved token values.
        MediaServicesCredentials credentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey)
        {
            AccessToken = accessToken,
            TokenExpiration = tokenExpiration
        };

        CloudMediaContext context2 = new CloudMediaContext(credentials);

    Hello hello Media Services SDK에서 업데이트 된 경우 hello 토큰 복사본을 업데이트 합니다. 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* Hello System.Collections.Concurrent.ConcurrentDictionary 컬렉션 (hello를 사용 하 여 MediaServicesCredentials 개체를 캐시할 수 있습니다 (예: 로드 공유 또는 전 세계 분산) 여러 미디어 서비스 계정이 있는 경우 ConcurrentDictionary 컬렉션을 나타냅니다 여러 스레드에서 동시에 액세스할 수 있는 키/값 쌍의 스레드로부터 안전한 컬렉션을). 그런 다음 hello GetOrAdd 메서드 tooget hello 캐시 된 자격 증명을 사용할 수 있습니다. 
  
        // Declare a static class variable of hello ConcurrentDictionary type in which hello Media Services credentials will be cached.  
        private static readonly ConcurrentDictionary<string, MediaServicesCredentials> mediaServicesCredentialsCache = 
            new ConcurrentDictionary<string, MediaServicesCredentials>();

        // Cache (or get already cached) Media Services credentials. Use these credentials toocreate a new CloudMediaContext object.
        static public CloudMediaContext CreateMediaServicesContext(string accountName, string accountKey)
        {
            CloudMediaContext cloudMediaContext;
            MediaServicesCredentials mediaServicesCredentials;

            mediaServicesCredentials = mediaServicesCredentialsCache.GetOrAdd(
                accountName,
                valueFactory => new MediaServicesCredentials(accountName, accountKey));

            cloudMediaContext = new CloudMediaContext(mediaServicesCredentials);

            return cloudMediaContext;
        }

## <a name="connecting-tooa-media-services-account-located-in-hello-north-china-region"></a>Hello 북 중국 지역에 있는 tooa 미디어 서비스 계정 연결
계정 hello 북 중국 지역에 있으면 hello 다음 생성자를 사용 합니다.

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

예:

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a>구성에서 연결 값 저장
것이 가장 좋습니다 toostore 연결 값, 특히 중요 한 값 예: 계정 이름 및 암호를 구성 합니다. 또한 것이 좋음 tooencrypt 중요 한 구성 데이터입니다. Hello Windows 파일 시스템 EFS (암호화)를 사용 하 여 hello 전체 구성 파일을 암호화할 수 있습니다. 파일을 마우스 오른쪽 단추로 클릭 hello 파일에서 EFS tooenable 선택 **속성**, hello에서 암호화를 사용 하도록 설정 하 고 **고급** 설정 탭 합니다. 또는 보호되는 구성을 사용하여 구성 파일에서 선택한 부분을 암호화하기 위해 사용자 지정 솔루션을 만들 수 있습니다. [보호되는 구성을 사용하여 구성 정보 암호화](https://msdn.microsoft.com/library/53tyfkaw.aspx)를 참조하세요.

다음 App.config 파일 hello hello 필수 연결 값을 포함 합니다. hello에 대 한 값을 hello <appSettings> 요소는 hello 미디어 서비스 계정 설정 프로세스에서 가져온 hello 필요한 값입니다.

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


구성에서 연결 값 tooretrieve hello를 사용할 수 있습니다 **ConfigurationManager** 클래스 하 고 코드에서 값 toofields hello를 할당 합니다.

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

