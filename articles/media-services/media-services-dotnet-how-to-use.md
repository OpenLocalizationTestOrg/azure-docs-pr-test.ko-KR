---
title: "aaaHow tooSet를 컴퓨터에.net 미디어 서비스 개발"
description: ".NET 용 미디어 서비스 SDK hello를 사용 하 여 미디어 서비스에 대 한 hello 필수 구성 요소에 알아봅니다. 또한 학습 방법을 toocreate Visual Studio 응용 프로그램입니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec2804c7-c656-4fbf-b3e4-3f0f78599a7f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: juliako
ms.openlocfilehash: a5a2af3211d8156fd7dea99831fb769df4130d41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-development-with-net"></a>.NET을 사용한 미디어 서비스 개발
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

이 항목에서는 방법을 toostart 개발 미디어 서비스.NET을 사용 하 여 응용 프로그램입니다.

hello **Azure 미디어 서비스.NET SDK** 라이브러리를 사용 하면.NET을 사용 하 여 미디어 서비스에 대해 tooprogram 합니다. 것에.net을 보다 쉽게 toodevelop hello toomake **Azure 미디어 서비스.NET SDK Extensions** 라이브러리가 제공 됩니다. 이 라이브러리는 .NET 코드를 단순화하는 일련의 확장 방법 및 도우미 함수를 포함합니다. 두 라이브러리 모두 **NuGet** 및 **GitHub**를 통해 사용할 수 있습니다.

## <a name="prerequisites"></a>필수 조건
* 신규 또는 기존 Azure 구독의 미디어 서비스 계정. Hello에 대 한 지침은 [어떻게 tooCreate Media Services 계정을](media-services-portal-create-account.md)합니다.
* 운영 체제: Windows 10, Windows 7, Windows 2008 R2 또는 Windows 8.
* .NET Framework 4.5.
* 있습니다.

## <a name="create-and-configure-a-visual-studio-project"></a>Visual Studio 프로젝트 만들기 및 구성
이 섹션에서는 Visual Studio에서 프로젝트 toocreate 미디어 서비스 개발을 위해 설정 합니다.  이 경우 hello 프로젝트는 C# Windows 콘솔 응용 프로그램 있지만 hello 여기에 표시 된 같은 설정 단계 적용 tooother 유형의 프로젝트 (예: Windows Forms 응용 프로그램 또는 ASP.NET 웹 응용 프로그램) 미디어 서비스 응용 프로그램에 대해 만들 수 있습니다.

이 섹션에서는 방법을 toouse **NuGet** tooadd 미디어 서비스.NET SDK extensions와 다른 종속 라이브러리입니다.

또는 GitHub에서 hello 최신 미디어 서비스.NET SDK 비트를 얻을 수 있습니다 ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) 또는 [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)) hello 솔루션을 빌드하고 hello 참조 toohello 클라이언트 프로젝트를 추가 합니다. 모든 hello 필요한 종속성을 다운로드 하 고 자동으로 추출 합니다.

1. Visual Studio를 사용하여 새 C# 콘솔 응용 프로그램을 만듭니다. Hello 입력 **이름**, **위치**, 및 **솔루션 이름**, 한 다음 확인을 클릭 합니다.
2. Hello 솔루션을 빌드하십시오.
3. 사용 하 여 **NuGet** tooinstall 추가 **Azure 미디어 서비스.NET SDK Extensions** (**windowsazure.mediaservices.extensions**). 이 패키지를 설치하면 **미디어 서비스 .NET SDK** 도 설치되고 다른 모든 필수 종속성이 추가됩니다.
   
    Hello 최신 버전의 NuGet이 설치 되어 있는지 확인 합니다. 자세한 내용 및 설치 지침은 [NuGet](http://nuget.codeplex.com/)을 참조하세요.
4. 솔루션 탐색기에서 hello hello 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 관리 하는 NuGet 패키지를 선택 합니다.
   
    hello NuGet 패키지 관리 대화 상자가 나타납니다.
5. Azure MediaServices Extensions 검색 hello 온라인 갤러리에서 Azure 미디어 서비스.NET SDK Extensions를 선택 하 고 hello 설치 단추를 클릭 합니다.
   
    hello 프로젝트가 수정 되 고 toohello 미디어 서비스.NET SDK Extensions, 미디어 서비스.NET SDK를 참조 하 고 다른 종속 어셈블리를 추가 합니다.
6. toopromote 클리너 개발 환경에서는 NuGet 패키지 복원을 활성화 하십시오. 자세한 내용은 [NuGet 패키지 복원"](http://docs.nuget.org/consume/package-restore)을 참조하세요.
7. 참조를 너무 추가**System.Configuration** 어셈블리입니다. 이 어셈블리는 hello System.Configuration을 포함합니다. **ConfigurationManager** 클래스 즉 tooaccess 사용 되는 구성 파일 (예를 들어 App.config).
   
    hello 참조 관리 대화 상자를 사용 하 여 tooadd 참조 hello 솔루션 탐색기에서에서 hello 프로젝트 이름을 마우스 오른쪽 단추로 클릭 합니다. 그런 다음 추가 및 참조를 선택합니다.
   
    hello 참조 관리 대화 상자가 나타납니다.
8. .NET framework 어셈블리에서 hello System.Configuration 어셈블리 찾기 선택한 확인 키를 누릅니다.
9. Hello App.config 파일을 열고 추가 된 *appSettings* 섹션 toohello 파일입니다.     
   
    Hello 값을 필요한 tooconnect toohello 미디어 서비스 API를 설정 합니다. 자세한 내용은 참조 [Azure AD 인증 액세스 hello Azure 미디어 서비스 API](media-services-use-aad-auth-to-access-ams-api.md)합니다. 

    사용 중인 경우 [사용자 인증](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) 구성 파일은 Azure AD 테 넌 트 도메인에 대 한 값 및 hello AMS REST API 끝점 때문일 수 있습니다.
    
    >[!Important]
    >대부분의 코드 샘플 hello Azure 미디어 서비스 설명서에에서 설정, 인증 tooconnect toohello AMS API의 사용자 (대화형) 형식을 사용 합니다. 이 인증 방법은 네이티브 앱(모바일 앱, Windows 앱 및 콘솔 응용 프로그램)의 관리 또는 모니터링에 적합합니다. 이 인증 방법은 서버, 웹 서비스, API 유형의 응용 프로그램에는 적합하지 않습니다.  자세한 내용은 참조 [Azure AD 인증 액세스 hello AMS API](media-services-use-aad-auth-to-access-ams-api.md)합니다.

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. Hello 기존 파일 덮어쓰기 **를 사용 하 여** hello 시작 부분에 코드 다음 hello로 hello Program.cs 파일의 문입니다.
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

이 시점에서 미디어 서비스 응용 프로그램을 개발 하는 준비 toostart 됩니다.    

## <a name="example"></a>예제

Toohello AMS API를 연결 하 고 사용 가능한 모든 미디어 프로세서를 나열 하는 작은 예제는 다음과 같습니다.
    
    class Program
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
    
        private static CloudMediaContext _context = null;
        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
    
            // List all available Media Processors
            foreach (var mp in _context.MediaProcessors)
            {
                Console.WriteLine(mp.Name);
            }
    
        }

##<a name="next-steps"></a>다음 단계

이제 [toohello AMS API를 연결할 수 있습니다](media-services-use-aad-auth-to-access-ams-api.md) 시작 [개발](media-services-dotnet-get-started.md)합니다.


## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

