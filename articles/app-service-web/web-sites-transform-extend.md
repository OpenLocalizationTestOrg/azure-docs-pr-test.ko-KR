---
title: "앱 서비스 웹 앱 aaaAzure 고급 구성 및 확장"
description: "Azure 앱 서비스 웹 앱과 tooadd 개인 확장 tooenable 사용자 지정 관리 작업에서 XML 문서 Transformation(XDT) 선언 tootransform hello ApplicationHost.config 파일을 사용 합니다."
author: cephalin
writer: cephalin
editor: mollybos
manager: erikre
services: app-service
documentationcenter: 
ms.assetid: b441a286-ef38-4abc-b102-cdb249baf5bc
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/25/2016
ms.author: cephalin
ms.openlocfilehash: 873347ac13113d1ac989cba29128382c81dcfcca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a>Azure 앱 서비스 웹 앱 고급 구성 및 확장
사용 하 여 [XML 문서 변환을](http://msdn.microsoft.com/library/dd465326.aspx) (XDT) 선언 hello를 변형할 수 있습니다 [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) Azure 앱 서비스의 웹 응용 프로그램에 파일입니다. 또한 XDT 선언 tooadd 개인 확장 tooenable 사용자 지정 웹 앱 관리 작업을 사용할 수 있습니다. 이 문서에는 웹 인터페이스를 통해 PHP 설정을 관리할 수 있는 샘플 PHP Manager 웹 앱 확장이 포함되어 있습니다.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a id="transform"></a>ApplicationHost.config를 통한 고급 구성
앱 서비스 플랫폼 hello 웹 응용 프로그램 구성에 대 한 유연성 및 제어를 제공합니다. Hello 표준 IIS ApplicationHost.config 구성 파일을 앱 서비스에서 직접 편집할 수 있도록 하지는 않지만 hello 플랫폼 XML 문서 변환 (XDT)에 기반 하는 선언적 ApplicationHost.config 변환 모델을 지원 합니다.

tooleverage이 변환 기능을 ApplicationHost.xdt 파일 사용 XDT 콘텐츠를 만들고 hello 사이트 루트 (d:\home\site) hello에 배치할 [Kudu 콘솔](https://github.com/projectkudu/kudu/wiki/Kudu-console)합니다. 변경 내용 tootake 효과 대 한 toorestart hello 웹 응용 프로그램을 할 수 있습니다.

hello applicationHost.xdt 샘플 다음 tooadd 새 사용자 정의 환경 변수 tooa PHP 5.4를 사용 하 여 응용 프로그램 웹 하는 방법을 보여 줍니다.

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.webServer>
    <fastCgi>
      <application>
        <environmentVariables>
          <environmentVariable name="CONFIGTEST" value="TEST" xdt:Transform="Insert" xdt:Locator="XPath(/configuration/system.webServer/fastCgi/application[contains(@fullPath,'5.4')]/environmentVariables)" />
        </environmentVariables>
      </application>
    </fastCgi>
  </system.webServer>
</configuration>
```

변환 상태 및 세부 정보는 로그 파일 hello FTP 루트 LogFiles\Transform에서 있습니다.

추가 샘플은 [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples)를 참조하세요.

**참고**<br />
요소 아래에서 모듈의 hello 목록에서 `system.webServer` 제거 하거나, 다시 정렬할 수는 있지만 추가 toohello 목록 수 있습니다.

## <a id="extend"></a> 웹앱 확장
### <a id="overview"></a> 개인 웹앱 확장 개요
앱 서비스는 관리 작업에 대한 확장성 지점으로 웹 앱 확장을 지원합니다. 실제로 일부 앱 서비스 플랫폼 기능은 사전 설치된 확장으로 구현됩니다. Hello 사전 설치 된 플랫폼 확장을 수정할 수 없지만, 동안 수 만들고 웹 앱에 대 한 개인 확장을 구성 합니다. 또한 이 기능은 XDT 선언이 있어야 사용할 수 있습니다. 개인 웹 앱 확장을 만들기 위한 주요 단계 hello hello 다음과 같습니다.

1. 웹앱 확장 **콘텐츠**: 앱 서비스에서 지원되는 웹 응용 프로그램 만들기
2. 웹앱 확장 **선언**: ApplicationHost.xdt 파일 만들기
3. 웹 앱 확장 **배포**: 콘텐츠 hello SiteExtensions 폴더 아래에 배치`root`

내부 링크 hello 웹 앱에 대 한 hello ApplicationHost.xdt 파일에 지정 된 tooa 경로 상대 toohello 응용 프로그램 경로 가리켜야 합니다. 모든 변경 toohello ApplicationHost.xdt 파일에는 웹 응용 프로그램 재활용이 필요합니다.

**참고**: 이 주요 요소에 대한 자세한 내용은 [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions)를 참조하세요.

자세한 예는 포함된 tooillustrate hello 단계를 만들고 개인 웹 앱 확장을 사용 하도록 설정 합니다. 소스 코드에서 다음과 같이 다운로드할 수 있는 hello PHP 관리자 예제에 대 한 hello [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager)합니다.

### <a id="SiteSample"></a> 웹앱 확장 예제: PHP Manager
PHP 관리자는 하면 웹 응용 프로그램 관리자가 tooeasily 보기 및 toomodify PHP.ini 파일을 직접 포함 하는 대신 웹 인터페이스를 사용 하 여 해당 PHP 설정을 구성 하는 웹 앱 확장 합니다. 프로그램 파일 및 hello 아래에 있는 hello php.ini 파일을 포함 하는 PHP에 대 한 공통 구성 파일입니다. 웹 앱의 hello 루트 폴더에 있는 user.ini 파일입니다. PHP 관리자 확장 hello hello를 사용 하 여 hello php.ini 파일 hello 앱 s 서비스 플랫폼에 직접 편집할 수 없기 때문입니다. 설정 변경 사항을 user.ini 파일 tooapply 합니다.

#### <a id="PHPwebapp"></a>hello PHP 관리자 웹 응용 프로그램
hello 다음은 PHP 관리자 배포 hello의 hello 홈 페이지:

![TransformSitePHPUI][TransformSitePHPUI]

웹 앱 확장 추가 ApplicationHost.xdt 파일 (hello ApplicationHost.xdt 파일에 대 한 자세한 내용은 사용 가능한 hello 다음의 섹션에는이 hello 웹 응용 프로그램의 hello 루트 폴더에 배치 되지만 일반 웹 응용 프로그램에서와 마찬가지로 볼 수 있듯이 문서)입니다.

PHP 관리자 확장이 hello hello Visual Studio ASP.NET MVC 4 웹 응용 프로그램 템플릿을 사용 하 여 만들어졌습니다. hello 솔루션 탐색기에서 다음 보기 hello의 구조를 표시 hello PHP 관리자 확장 합니다.

![TransformSiteSolEx][TransformSiteSolEx]

hello만 특별 한 논리 파일 I/O에 필요한는 tooindicate hello wwwroot hello 웹 앱의 디렉터리가 있는 합니다. Hello 다음 코드 예제와 hello 환경 변수 "HOME"으로 웹 응용 프로그램의 루트 경로 hello와 "site\wwwroot"를 추가 하 여 hello wwwroot 경로 생성할 수를 나타냅니다.

```csharp
/// <summary>
/// Gives hello location of hello .user.ini file, even if one doesn't exist yet
/// </summary>
private static string GetUserSettingsFilePath()
{
  var rootPath = Environment.GetEnvironmentVariable("HOME"); // For use on Azure Websites
  if (rootPath == null)
  {
    rootPath = System.IO.Path.GetTempPath(); // For testing purposes
  };
  var userSettingsFile = Path.Combine(rootPath, @"site\wwwroot\.user.ini");
  return userSettingsFile;
}
```


Hello 디렉터리 경로 사용 하는 다음 일반 파일 I/O 작업 tooread를 사용할 수 있으며 toofiles 작성.

웹 앱 확장 된 주의의 한 위치 내부 링크의 hello 처리를 인식합니다.  웹 앱에 절대 경로 toointernal 링크를 제공 하는 HTML 파일에 있는 모든 링크가 있으면 프로그램 루트로 확장 이름으로 이러한 링크는 앞에 추가 확인 해야 합니다. 이 과정이 필요 확장 프로그램에 대 한 hello 루트는 이제 "/`[your-extension-name]`/" 되지 않고 단지 "/", 따라서 모든 내부 링크를 업데이트 해야 적절 하 게 합니다. 예를 들어 코드에 링크 toohello 다음과 같은 있다고 가정 합니다.

`"<a href="/Home/Settings">PHP Settings</a>"`

Hello 링크 웹 앱 확장의 일부 이면 hello 링크 hello 다음 형식 이어야 합니다.

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

상대 경로 또는 웹 응용 프로그램 내에서 hello를 사용 하 여 ASP.NET 응용 프로그램의 대/소문자를 hello에 사용 하 여이 요구 사항을 해결할 수 있습니다 `@Html.ActionLink` 메서드 hello 적절 한 링크를 만듭니다.

#### <a id="XDT"></a>hello applicationHost.xdt 파일
웹 앱 확장에 대 한 hello 코드 %HOME%\SiteExtensions에서로 이동\[your 확장 이름]. 이 hello 확장 루트를 라고 합니다.  

tooregister tooplace hello 확장 루트에서 ApplicationHost.xdt 라는 파일을 필요한 hello applicationHost.config 파일에 웹 앱 확장 합니다. hello ApplicationHost.xdt 파일의 내용을 hello 다음과 같아야 합니다.

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.applicationHost>
    <sites>
      <site name="%XDT_SCMSITENAME%" xdt:Locator="Match(name)">
        <!-- NOTE: Add your extension name in hello application paths below -->
        <application path="/[your-extension-name]" xdt:Locator="Match(path)" xdt:Transform="Remove" />
        <application path="/[your-extension-name]" applicationPool="%XDT_APPPOOLNAME%" xdt:Transform="Insert">
          <virtualDirectory path="/" physicalPath="%XDT_EXTENSIONPATH%" />
        </application>
      </site>
    </sites>
  </system.applicationHost>
</configuration>
```

확장 이름으로 선택 하는 hello 이름에는 확장 루트 폴더와 이름과 같은 이름을 hello를 여야 합니다.

이 인해 새 응용 프로그램 경로 toohello 추가 hello 영향 `system.applicationHost` hello SCM 사이트에서 사이트 목록입니다. hello SCM 사이트는 특정 액세스 자격 증명으로는 사이트 관리 끝점입니다. 에 hello URL `https://[your-site-name].scm.azurewebsites.net`합니다.  

```xml
<system.applicationHost>
  ...       
  <sites>
    <site name="~1[your-website]" id="1716402716">
      <bindings>
        <binding protocol="http" bindingInformation="*:80: [your-website].scm.azurewebsites.net" />
        <binding protocol="https" bindingInformation="*:443: [your-website].scm.azurewebsites.net" />
      </bindings>
      <traceFailedRequestsLogging enabled="false" directory="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\LogFiles" />
      <detailedErrorLogging enabled="false" directory="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\LogFiles\DetailedErrors" />
      <logFile logSiteId="false" />
      <application path="/" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="D:\Program Files (x86)\SiteExtensions\Kudu\1.24.20926.5" />
      </application>
      <!-- Note hello custom changes that go here -->
      <application path="/[your-extension-name]" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\SiteExtensions\[your-extension-name]" />
      </application>
    </site>
  </sites>
  ... 
</system.applicationHost>
```

### <a id="deploy"></a> 웹앱 확장 배포
tooinstall 웹 앱 확장을 웹 응용 프로그램 toohello의 모든 hello 파일 FTP toocopy를 사용할 수 있습니다 `\SiteExtensions\[your-extension-name]` tooinstall hello 확장 원하는 hello 웹 응용 프로그램의 폴더입니다.  있는지 toocopy hello ApplicationHost.xdt 파일 toothis도 위치 수입니다. 웹 앱 tooenable hello 확장 프로그램을 다시 시작 합니다.

웹 앱 확장 프로그램에 수 toosee 수 있어야 합니다.

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

URL 처럼 보이는 hello URL 웹 앱에 대 한 HTTPS를 사용 하 고 ".scm"를 포함 한다는 해당 hello를 note 합니다.

Hello 키가 있는 응용 프로그램 설정을 추가 하 여 개발 및 조사를 수행 하는 동안 웹 앱에 대 한 확장 가능한 toodisable 모든 개인 (사전 설치 되지) 되었기 `WEBSITE_PRIVATE_EXTENSIONS` 값 `0`합니다.

> [!NOTE]
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
> 
> 

## <a name="whats-changed"></a>변경된 내용
* 웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

