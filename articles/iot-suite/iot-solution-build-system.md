---
title: "MyDriving Azure IoT 예제: 빌드하기 | Microsoft Docs"
description: "앱을 빌드하는 방법의 전체 데모를 tooarchitect 스트림 분석, 기계 학습 및 이벤트 허브를 포함 하 여 Microsoft Azure를 사용 하 여 프로그램 IoT 시스템."
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: c2fcd6ee-3bbe-43d1-a066-dce52cc3a53d
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 06/30/2017
ms.author: harikm
ms.openlocfilehash: e78571225697f745fe011c722e57c8600704c392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-hello-mydriving-solution-tooyour-environment"></a>빌드 및 hello MyDriving 솔루션 tooyour 환경 배포
MyDriving은 자동차에서 데이터를 수집하고, 기계 학습을 사용하여 처리한 후 휴대폰에 표시하는 사물 인터넷(IoT) 솔루션입니다. 다양 한 Microsoft Azure에서 제공 하는 서비스의 hello 백 엔드로 구성 됩니다. 클라이언트 hello, Android, iOS 또는 Windows 10 휴대폰 될 수 있습니다.

Hello MyDriving 솔루션 toogive 만든 사용자 고유의 IoT 시스템 만들기에 대 한 자세한 내용은 있습니다. Hello에서 [GitHub의 리포지토리 MyDriving](https://github.com/Azure-Samples/MyDriving), Azure 계정에 Azure 리소스 관리자 스크립트 toodeploy hello 백 엔드 아키텍처를 얻을 수 있습니다. 해당 지점에서 hello 서로 다른 서비스를 다시 구성, hello 쿼리 toosuit 직접 데이터를 수정 및 등 수 있습니다. -Hello 모바일 앱, hello Azure 앱 서비스 API 프로젝트 등에-hello MyDriving 리포지토리에 코드와 함께 이러한 스크립트를 찾을 수 있습니다.

Hello에서 hello 앱을 아직 시도 하지 않은 경우 확인 [Get 시작된 가이드](iot-solution-get-started.md)합니다.

Hello에 hello 아키텍처의 자세한 계정이 [MyDriving 참조 가이드](http://aka.ms/mydrivingdocs)합니다. 요약 하자면에 여러 단계는 설정 toocreate 비슷한 프로젝트:

* **클라이언트 앱**은 Android, iOS 및 Windows 10 휴대폰에서 실행됩니다. Xamarin 플랫폼 tooshare hello 사용 하 여 대부분 GitHub 아래에 저장 되어 있는 hello 코드 `src/MobileApp`합니다. hello 앱 실제로 두 가지 고유 함수를 수행합니다.
  * 자체 위치 서비스 toohello 시스템의 클라우드 백 엔드와 hello 통합 진단 프로그램 (OBD) 장치에서 원격 분석을 릴레이합니다.
  * 사용자가 자신의 기록된 주행 기록에 대해 쿼리할 수 있는 사용자 인터페이스입니다.
* A **클라우드 서비스** hello 주행 데이터를 실시간으로 수집 하 고 처리 합니다. 이 서비스를 만드는 hello 주 작업 toochoose, 매개 변수화 및 다양 한 Azure 서비스를 연결 합니다. Hello 파트의 일부 스크립트 toofilter 및 프로세스 hello 들어오는 데이터가 필요합니다. Azure 리소스 관리자 템플릿 tooconfigure 모든 hello 부분 사용합니다.
* A **모바일 서비스 앱** hello 장치 응용 프로그램의 hello 사용자 인터페이스 부분 뒤 hello 웹 서비스입니다. 주요 작업은 저장, 처리 된 데이터의 tooquery hello 데이터베이스입니다. 해당 코드는 GitHub에서 `src/MobileAppService`아래에 있습니다.
* **Xamarin이 포함된 Visual Studio** 가 개발 환경입니다. Visual Studio의 구성 요소와 독립 실행형 통합된 개발 환경 (IDE) 모두 있는 Xamarin 사용 되는 toobuild hello 장치 플랫폼 간 코드입니다. toobuild hello iOS는 필요한 toohave OS X 컴퓨터에서 실행 되는 Xamarin의 인스턴스. 필요한 경우 Visual Studio에서 관리하는 에이전트로 실행될 수 있습니다.
* **단위 테스트** hello 장치의 앱 Xamarin 테스트 클라우드에서 수행 됩니다.
* **GitHub** hello 리포지토리 hello 코드, 스크립트 및 서식 파일을 저장 했습니다.
* **Visual Studio Team Services** 는 클라우드 서비스가 toomanage hello 연속 빌드 및 테스트 hello 웹 서비스와 장치 응용 프로그램의 사용입니다.
* **HockeyApp** hello 장치 코드에 사용 되는 toodistribute 릴리스의 됩니다. 또한 충돌 및 사용 보고서 및 사용자 피드백을 수집합니다.
* **Visual Studio Application Insights** 모니터 hello 모바일 웹 서비스입니다.

이제 이 모든 항목을 설정하는 방법을 살펴보겠습니다. 

> [!NOTE] 
> 다양 한 단계를 수행 하는 hello는 선택적입니다.
>
>

## <a name="sign-up-for-accounts"></a>계정 등록
* [Visual Studio Dev Essentials](https://www.visualstudio.com/products/visual-studio-dev-essentials-vs.aspx). 이 무료 프로그램에 쉽게 액세스할 수 있도록 toomany 개발자 도구 및 Visual Studio, Visual Studio Team Services 및 Azure를 포함 한 서비스를 제공 합니다. 12개월 동안 Azure에서 월간 $25 크레딧을 부여합니다. 구독 tooPluralsight 교육 및 Xamarin 대학도 포함 됩니다. [Azure](https://azure.com) 및 [Visual Studio Team Services](https://www.visualstudio.com/products/visual-studio-team-services-vs.aspx)의 무료 계층과 별도로 등록할 수도 있으나 이 경우 Azure 크레딧은 제공되지 않습니다.
* [HockeyApp](https://rink.hockeyapp.net/) (선택 사항) - 모바일 앱의 테스트 배포를 관리하고 원격 분석을 수집합니다.
* [Xamarin](https://xamarin.com/) (필수) hello 모바일 앱을 실행 중인 디버그 실행 및 테스트를 작성 하기 위한 [Xamarin 테스트 클라우드](https://xamarin.com/test-cloud)합니다.
* [GitHub](https://github.com/Azure-Samples/MyDriving/) (선택 사항) toocreate 무료 공용 저장소 (개인 저장소는 유료) 사용자 고유의 코드에 대 한 합니다. 또는 개인 저장소에 대 한 Visual Studio Team Services에서 hello 기본 계획을 사용할 수 있습니다.
* [Power BI](https://powerbi.microsoft.com/) hello 전체 시스템에서 데이터의 toocreate 풍부한 시각화 (선택 사항).

> [!NOTE]
> GitHub 계정 tooaccess hello MyDriving 코드에 필요 하지 않습니다 [GitHub MyDriving 리포지토리 hello](https://github.com/Azure-Samples/MyDriving)합니다.
> 
> 

## <a name="install-development-tools"></a>개발 도구 설치
hello 다음 설치 프로그램은 hello 전체 솔루션을 개발 하기 위한:는 iOS, Android 및 Windows 10 Mobile에는 Azure 플랫폼 간 앱 백 엔드 합니다.

대신 Azure 다시 종료 hello에서 작동 하지 않는 경우 Mac 또는 Windows toodevelop hello 모바일 앱에 Xamarin Studio 사용할 수 있습니다.

[이 설치 프로그램에 대한 자세한 설명](https://msdn.microsoft.com/library/mt613162.aspx)이 있습니다.

### <a name="windows-development-machine"></a>Windows 개발 컴퓨터
windows hello 중앙 집중식 도구는 Visual Studio hello MyDriving 앱 Android 및 Windows, hello 앱 서비스 API 프로젝트 및 마이크로 서비스 확장에 대 한 작업 수입니다.

Xamarin, Git, 에뮬레이터 및 기타 유용한 구성 요소가 Visual Studio에 모두 통합되어 있습니다.

설치:

* [Xamarin 포함 Visual Studio](https://www.visualstudio.com/products/visual-studio-community-vs) (모든 버전--커뮤니티는 무료)
* [범용 Windows 플랫폼용 SQLite](https://visualstudiogallery.msdn.microsoft.com/4913e7d5-96c9-4dde-a1a1-69820d615936). Toobuild hello Windows 10 Mobile 코드가 필요 합니다.
* [Azure SDK for Visual Studio](https://www.visualstudio.com/vs/azure-tools/) Azure를 관리 하기 위한 명령줄 도구와 함께 Azure에서 응용 프로그램을 실행 하기 위한 SDK hello를 제공 합니다.
* [Azure 서비스 패브릭 SDK](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric). 필요한 toobuild hello [마이크로 서비스](../service-fabric/service-fabric-get-started.md) 확장 합니다.

Hello 오른쪽 Visual Studio 확장 있어야 합니다. **도구** 아래를 확인해 보면 **Android, iOS, Xamarin…**이 표시됩니다. 그렇지 않은 경우 Visual Studio를 열고, Xamarin을 검색 및 hello 프롬프트 tooinstall 따라 것입니다. 또한 **Windows용 Git**이 설치되어 있는지도 확인합니다. Visual Studio에서 그렇지 않은 경우에 검색 하 고 hello 프롬프트 tooinstall 따라 것입니다. 

### <a name="mac-development-machine"></a>Mac 개발 컴퓨터
hello Mac (Yosemite 이상 버전)는 iOS 용 toodevelop를 원하는 경우에 필요 합니다. Windows toodevelop에서 Xamarin을 사용한 Visual Studio를 사용 하 고 모든 hello 코드 관리를 있지만 Xamarin 순서 toobuild에서 Mac에 설치 된 에이전트를 사용 하 고 기호 hello iOS 코드입니다.

![Windows에서 개발 및 Mac에서 빌드](./media/iot-solution-build-system/image1.png)

(대신 사용할 수 있습니다 Xamarin Studio hello Mac toodevelop 플랫폼 간 앱에서 직접.)

대상 플랫폼으로 iOS tooinclude 않으려면 hello Mac 필요는 없습니다.

설치:

* [iOS용 Xamarin Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/mac/). Windows 가상 컴퓨터를 실행하는 Mac에서 Visual Studio 및 Xamarin을 설정할 수도 있습니다. MSDN의 [Mac 사용자용 설정, 설치 및 확인](https://msdn.microsoft.com/library/mt488770.aspx) 을 참조하세요.
* [Azure 개발 도구](https://azure.microsoft.com/downloads/) (선택 사항).

Mac. hello에 대 한 원격 로그인을 사용 하도록 설정 **시스템 기본 설정** > **공유**를 연 다음 **원격 로그인**을 선택합니다.

Windows에서 Visual Studio에서 iOS 프로젝트를 열 때 플러그 인 Xamarin hello 묻는 메시지가 나타납니다 hello Mac.의 hello ID에 대 한

## <a name="fetch-hello-github-repository"></a>Hello GitHub 리포지토리를 인출 합니다.
로컬 복사본을 가져올 [GitHub MyDriving 리포지토리 hello](https://github.com/Azure-Samples/MyDriving) hello를 사용 하 여 **zip 파일 다운로드** GitHub, Visual Studio 또는 다른 Git 클라이언트에서 단추입니다.

짧은 경로 이름을 사용할 경우 예: c: hello 파일 tooa 폴더의 압축을 푸는\\코드입니다.

또는와 toodate tookeep를 싶거나 tooour 코드 적용할 hello 리포지토리를 복제 다음과 같습니다.

**git clone https://github.com/Azure-Samples/MyDriving.git**

## <a name="get-a-bing-maps-api-key"></a>Bing 지도 API 키 가져오기
[Bing 지도 API 키를 등록합니다](https://msdn.microsoft.com/library/ff428642.aspx).

22에서 줄이 tooreplace 필요한 `src/MobileApps/MyDriving/MyDriving.Utils/Logger.cs`합니다.

## <a name="build-hello-demo-app"></a>Hello 데모 응용 프로그램 빌드
Visual Studio에서 이러한 솔루션을 엽니다.

* src\MobileApps\MyDriving.sln
* src\MobileAppService\MyDrivingService.sln
* src\Extensions\ServiceFabric\VINLookUpApplication\VINLookUpApplication.sln

다음과 같은 프롬프트가 표시됩니다.

* 잠재적으로 신뢰할 수 없는 프로젝트를 신뢰합니다. Tooopen 선택 toogo 계속 하려는 경우.
* 새로운 Windows 10 컴퓨터에서 작업하는 경우 개발자 모드를 설정합니다.
* Xamarin 자격 증명을 제공합니다.
* Xamarin Mac. toohello 연결 Mac를 설정 하지 않은 경우 마우스 오른쪽 단추로 클릭 hello iOS Visual Studio에서 프로젝트를 선택한 후 **프로젝트 언로드**합니다.

Hello 솔루션을 다시 빌드하십시오.

작성 하는 데 문제가 있는 경우 आ म क ा hello 솔루션 tooquirks를 시도해 보십시오.

* *VINLookupApplication 프로젝트 로드 되지 않습니다*: hello 설치 되어 있는지 확인 [Azure SDK for Visual Studio](https://www.visualstudio.com/vs/azure-tools/)합니다.
* *서비스 패브릭 프로젝트 빌드되지 않으면*: hello 인터페이스 프로젝트를 먼저 빌드하고 hello 서비스 패브릭 SDK 설치 되어 있는지 확인 합니다.
* *Android 앱이 빌드되지 않음*:
  
  * **도구** > **Android** > **Android SDK Manager**를 열고 Android 6(API 23)/SDK 플랫폼이 설치되어 있는지 확인합니다.
  * 다음 디렉터리를 삭제한 다음 다시 빌드합니다.<br/>
    `%LocalAppData%\Xamarin\zips`

## <a name="get-tooknow-hello-code"></a>Tooknow hello 코드 가져오기
Hello 솔루션에서 다음을 확인할 수 있습니다.

* Azure 확장: 서비스 패브릭.
* Azure HDInsight: Azure에서 주행 데이터를 처리하는 스크립트.
* 모바일 앱: hello 장치 앱입니다.
* MobileAppsService/MyDrivingService: hello 웹 다시 종료 합니다.
* Power BI: hello 보고서 정의입니다.
* Scripts:
  
  * 리소스 관리자: 템플릿 toobuild hello Azure 리소스입니다.
  * PowerShell: toorun hello 리소스 관리자 템플릿을 스크립팅합니다.
  * Azure SQL 데이터베이스: 데이터베이스 디버깅.
* SQL 데이터베이스: CreateTables: 스키마 정의.
* Azure 스트림 분석: 변환 hello 들어오는 데이터 스트림에 쿼리합니다.

## <a name="run-hello-apps-in-development-mode"></a>Hello 앱 개발 모드에서 실행
작업 toorun hello 응용 프로그램을 사용 하는 hello 장치를 기반으로 수행 합니다.

* 백 엔드: 집합 MyDrivingService hello 시작 프로젝트 및 F5 toorun hello 백 엔드 웹 서비스 키를 누릅니다. Hello API 목록 브라우저 보기를 열립니다.
* 모바일 클라이언트: hello [모바일 응용 프로그램 모두 Xamarin 개발 방식을](https://developer.xamarin.com/guides/cross-platform/deployment,_testing,_and_metrics/debugging_with_xamarin/)합니다.
  
  * Android: 자세한 내용은 [Xamarin에서 Android 디버깅](http://developer.xamarin.com/guides/android/deployment,_testing,_and_metrics/debugging_with_xamarin_android/)을 참조하세요.
  * iOS: 자세한 내용은 [iOS에서 디버깅](http://developer.xamarin.com/guides/ios/deployment,_testing,_and_metrics/debugging_in_xamarin_ios/)을 참조하세요.
  * Windows Phone: 자세한 내용은 [Xamarin + Windows Phone](https://developer.xamarin.com/guides/cross-platform/windows/phone/)을 참조하세요.

## <a name="upload-hello-mobile-app-toohockeyapp"></a>Hello 모바일 앱 tooHockeyApp 업로드
HockeyApp 신작의 사용자에 게 알리는 Android, iOS 또는 Windows 앱 tootest 사용자의 hello 배포를 관리 합니다. 또한 유용한 충돌 보고서, 스크린샷을 포함한 사용자 피드백, 사용 현황 메트릭도 수집합니다.

[업로드하여 시작](http://support.hockeyapp.net/kb/app-management-2/how-to-create-a-new-app) 합니다. 그런 다음 역시 로그인[HockeyApp](https://rink.hockeyapp.net) 개발 컴퓨터에서 합니다. Hello 개발자 대시보드에서 **새 앱**, 한 다음 작성 하는 hello 파일 hello 창으로 끕니다. (이상 버전에서는 자동화할 수 있습니다 빌드 서비스 toodo이.)

이제 앱 대시보드가 표시됩니다.

![Hello 응용 프로그램 대시보드에서 개요 탭](./media/iot-solution-build-system/image2.png)

앱에서 실행 되는 각 플랫폼에 대 한 hello 프로세스를 반복 합니다. 다음을 수행할 수 있습니다 hello 다음:

* 사용 하 여 hello [앱 ID](http://support.hockeyapp.net/kb/app-management-2/how-to-find-the-app-id) hello 대시보드 toosend 충돌 데이터 및 응용 프로그램의 의견도 있습니다. MyDriving, src/MobileApps/MyDriving/MyDriving.Utils/Logger.cs에 hello Id를 업데이트 합니다.
* [테스트 사용자를 초대합니다](http://support.hockeyapp.net/kb/app-management-2/how-to-invite-beta-testers). 테스터 사용자를 URL toorecruit를 가져옵니다. 팀에 대해 수 toosign 여야 하며, hello 앱을 다운로드, 피드백을 보낼 합니다.
* 보다 개방적 베타 릴리스 버전 사용 하려는 경우 hello 배포 toopublic를 설정 합니다. **Manage App** > **Distribution** > **Download = Public**을 클릭합니다. 이제 모든 사용자가 앱을 다운로드하고 피드백을 보낼 수 있으며 새 버전이 게시되면 알림을 보게 됩니다. 또한 충돌 보고서도 받을 수 있습니다.
  
   ![Hello 대시보드에서 팀](./media/iot-solution-build-system/image3.png)
* [링크 크래시 보고 tooVisual Studio Team Services](http://support.hockeyapp.net/kb/third-party-bug-trackers-services-and-webhooks/how-to-use-hockeyapp-with-visual-studio-team-services-vsts-or-team-foundation-server-tfs)합니다. **Manage App** > **Visual Studio Team Services**를 클릭합니다. HockeyApp은 충돌 보고서가 있거나 피드백을 받으면 Team Services에 작업 항목을 자동으로 만들 수 있습니다.

Hello에서 더 읽기 [HockeyApp 사이트](https://hockeyapp.net)합니다.

## <a name="test-hello-mobile-app-on-xamarin-test-cloud"></a>Xamarin 테스트 클라우드 테스트 hello 모바일 앱
[Xamarin 테스트 클라우드](https://developer.xamarin.com/guides/testcloud/introduction-to-test-cloud/) hello 클라우드에서 실제 장치에서 UI 테스트를 자동화 합니다. Hello NUnit 프레임 워크를 사용 하 여 hello 사용자 인터페이스를 통해 앱을 실행 하는 테스트를 작성 합니다.

hello 통합 Xamarin toouse [Xamarin.UITests](https://developer.xamarin.com/guides/testcloud/uitest/intro-to-uitest/) NuGet 패키지로 제공 앱에 대 한 SDK입니다. Hello 데모 응용 프로그램에서 찾을 수 있으며 템플릿을 만들 때 새 테스트 프로젝트 hello로 Xamarin 포함 했습니다.

![여기서 toofind hello hello 인터페이스에 플랫폼 SDK](./media/iot-solution-build-system/image4.png)

예제 테스트 프로젝트 hello 앱 hello 리포지토리에 포함 되어 있습니다. [MyDriving](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileAppService)에서 [src](https://github.com/Azure-Samples/MyDriving/tree/master/src)/MobileApps/[MyDriving](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileApps/MyDriving)/MyDriving.UITests/를 살펴봅니다.

Visual Studio Team Services 빌드를 사용 하는 경우 쉽게 toowrite Xamarin UI 단위 테스트를 빌드의 일부로 실행할 됩니다.

## <a name="deploy-azure-services"></a>Azure 서비스 배포
Azure 서비스 및 서비스 팀 빌드 서비스의 자동 배포 tooperform toohello 참조에 필요한 세부 정보 **scripts/README.md**합니다.

Microsoft Azure toobuild 클라우드 응용 프로그램을 사용할 수 있는 다양 한 서로 다른 서비스를 제공 합니다. 연결 하는 최상의 경우에는에서 개별적으로 (예: 응용 프로그램 서비스/웹 응용 프로그램) 사용할 수 있습니다, 있지만 하기가 tooform 통합된 시스템을 사용 하 여 MyDriving에 있습니다.

가능한 toocreate 되 고 Azure 서비스를 수동으로 상호 연결 이지만 toouse Azure 리소스 관리자 템플릿을 훨씬 빠르고 안정적 수 있습니다. [리소스 관리자](../azure-resource-manager/resource-group-overview.md) hello 배포 솔루션의 리소스와 서로 hello 상호 연결을 만드는 작업을 자동화 합니다.

아래 hello GitHub 리포지토리에 hello MyDriving 시스템에 대 한 hello 서식 파일을 찾을 수 [스크립트/ARM](https://github.com/Azure-Samples/MyDriving/tree/master/scripts/ARM)합니다. Hello 여러 서비스 가이드의 아키텍처에 연결 되는 방식의 포괄적이 고 간결한 뷰를 제공 합니다. 이러한 모든 hello에 자세히 설명 [MyDriving 참조 가이드](http://aka.ms/mydrivingdocs), 하지만 많은 hello 템플릿 자체를 읽는 것 만으로도 알아볼 수 있습니다.

> [!NOTE]
> 대부분의 Azure 서비스는 hello 가격 책정 계층에 따라 표시 되는 연관된 비용입니다. 새 tooAzure 인 경우 다음을 할 수 있습니다 [무료로 사용해 보세요](https://azure.microsoft.com/free/)합니다. 그러나 계획이 없으면 toouse hello MyDriving 시스템에서에서 특정 구성 요소, 수 있는지 tooremove tooavoid 헤드 비용을 합니다. hello "예상 운영 비용" 섹션 나중에이 문서의 제공 일반적인 서비스 비용의 요약 합니다.
> 
> 

### <a name="edit-hello-template"></a>Hello 템플릿 편집
toocustomize, 배포 시나리오의 복사본을 먼저 확인, 아마도 tooremove 필요 없는 구성 요소 또는 tooadd 다른\_complete.params.json 및 시나리오\_complete.json toomake 변경 된 합니다.

Hello 시나리오를 사용할 수\_다양 한 기본 값, 같은 hello 서비스 SKU 또는 hello 저장소 복제 유형으로 다음 표에 hello에 설명 된 대로 complete.params.json 파일 toooverride 합니다. hello 기본값 hello 가장 저렴 한 비용 옵션을 선택합니다.

| **매개 변수** | **설명** | **기본값** |
| --- | --- | --- |
| IoT Hub SKU |Azure IoT Hub 서비스에 대한 계층 |F1 |
| 저장소 계정 유형 |저장소 복제 유형 |표준 LRS |
| SQL 서비스 목표 |동시성 슬롯 사용량 |DW100 |
| 호스팅 계획 SKU |앱 서비스에 대한 서비스 계획 |F1 |

scenario\_complete.json에서

* "기본 이름이"를 검색 하 고 원하는 tooa 이름을 변경 합니다.
* "만들기"를 검색합니다. 각 섹션에서 리소스를 만듭니다.
* SqlServerAdminLogin 및 sqlServerAdminPassword toosuitable 값을 설정 합니다.
* 리소스를 만듭니다 하는 섹션을 삭제 하기 전에 hello 파일의 다른 위치에서 해당 이름을 검색 하 여 참조 하는 셀에 있는지 여부를 확인 합니다. 서비스를 만드는 각 섹션에는 해당 종속성을 나열하는 *dependsOn* 섹션이 있습니다.

여기의 hello 템플릿을 구성 합니다. 세부 정보는 hello에서 [참조 가이드](http://aka.ms/mydrivingdocs)합니다.

| **서비스** | **설명 및 세부 정보** |
| --- | --- |
| 저장소 계정 |hello 템플릿은 3 개의 계정을 만듭니다. |
| -SQL 데이터베이스 A 스트림 분석에서 집계 된 원격 분석을 수신 하 고 역할을 API 끝점을 통해이 데이터를 노출 하는 Azure 앱 서비스 테이블에 대 한 hello 백업 저장소입니다. | |
| HDInsight에서 처리 toobe 다른 스트림 분석 작업에서 기록 데이터를 누적 하는 blob 저장소입니다. | |
| - SQL Database: HDInsight에서 Power BI에 사용하기 위해 처리한 결과를 수신합니다. | |
| Azure IoT Hub |양방향 연결 tooeach 연결 된 장치를 설정합니다. Hello MyDriving 솔루션, hello 모바일 응용 프로그램 역할을 필드 게이트웨이 toosend 데이터 tooAzure IoT Hub 합니다. Azure IoT 허브는 다음 분석 하는 입력된 tooStream로 사용 됩니다. |
| Azure Event Hubs |Azure Service Fabric을 사용 하 여 만든 tooextensions를 출력 하는 hello 큐에 대기 시키는 스트림 분석 작업에 대 한 출력입니다. |
| Azure SQL 데이터 웨어하우스 | |
| 스트림 분석 작업 |사용 되는 tooaggregate 쿼리를 입력 및 출력 연결 hello 앱 서비스 Api, Azure 기계 학습, 확장 및 Power BI에 대 한 실시간 및 과거 데이터입니다. |
| 기계 학습 작업 영역 |실험, R 코드, API 서비스를 포함합니다. |
| Azure 데이터 팩터리 |예약된 기계 학습 재학습입니다. |
| 서비스 패브릭 호스팅 계획 |확장용 |
| 앱 서비스("모바일 앱") |Hello 모바일 앱에 대 한 끝점을 제공 하는 호스트 hello 모바일 앱 API 프로젝트입니다. hello API 코드는 Visual Studio에서 서비스 배포 tooApp 이어야 합니다. |
| 경고 규칙 |Hello 앱 응답 오류가 표시 하는 경우 사용자의 전자 메일을 보냅니다. |
| Application Insights |Hello 앱 서비스의 Api의 성능을 모니터링 합니다. Visual Studio에서 tooconfigure hello 연결을 해야 합니다. |
| Azure 키 자격 증명 모음 |Hello 웹 서비스 클러스터 인증서를 저장 합니다. |

### <a name="run-hello-template"></a>Hello 템플릿을 실행합니다
**scripts/README.md**, 실행 중인 hello 서식 파일에 대 한 자세한 지침은 합니다.

tooprovision hello 스크립트를 사용 하 여 Azure 계정에서 이러한 모든 서비스 중 하나를 수행 다음 hello:

* PowerShell 사용:
  
  ```
  
  cd scripts/PowerShell;
  deploy.ps1 *location* *resourceGroupName*
  ```
  
  * *위치* 는 hello [는 Azure 위치](https://azure.microsoft.com/regions/)와 같은 `North Europe` 또는 `West US`합니다. 사용 하 여 `Get-AzureLocation` toofind 사용 가능한 위치의 목록입니다.
  * *resourceGroupName* toogive toohello 그룹에 속하는 모든 hello 리소스 hello 이름입니다. Hello 리소스와 완료 된 경우 삭제할 수 있습니다 이러한 모두 함께이 그룹을 삭제 하 여 합니다.
* Bash로 DeploymentScripts/Bash/deploy.sh를 실행합니다.
* 페이지를 열고 DeploymentScripts/VS/DeployARM.sln hello Visual Studio 솔루션을 빌드하십시오.

Note 각 시간 hello 템플릿이 실행 될, 새 이름으로 새 리소스 집합을 만듭니다. toodelete hello 리소스 toohello 포털 이동한 다음 hello 리소스 그룹을 삭제 합니다.

Hello 스크립트 어떤 이유로 든 실패할 경우 다시 실행할 수 있습니다.

Visual Studio Team Services에서 연속 통합을 구성 하는 옵션을 hello hello 스크립트 제공 합니다. Team Services 프로젝트를 설정하면 URL: https://yourAccountName.visualstudio.com이 생깁니다. 묻는 경우 hello 전체 URL을 입력 합니다. Team Services 프로젝트에 대한 기존 또는 신규 이름을 지정할 수 있습니다.

## <a name="set-up-build-and-test-definitions-in-visual-studio-team-services"></a>빌드를 설정하고 Visual Studio Team Services에서 정의를 테스트합니다.
이 프로젝트에서는 대부분 빌드 및 테스트 기능을 위해 Team Services를 사용합니다. 하지만 Kanban 보드를 사용한 작업 관리, 작업 및 소스 제어와 통합된 코드 검토 및 제어 빌드와 같은 뛰어난 공동 작업 지원도 제공합니다. GitHub, Xamarin, HockeyApp, 물론 Visual Studio와 같은 다른 도구와도 잘 통합됩니다. Hello 웹 인터페이스를 통해 또는 Visual Studio를 통해 액세스할 수 있습니다, 언제 든 지 더 편리 중에서 더 합니다.

릴리스 정의 다양 한 hello Team Services에서 사용할 수 있는 플러그 인 서비스를 사용 하 여 hello hello 빌드에서 단계 [마켓플레이스](https://marketplace.visualstudio.com/VSTS)합니다. 또한 toobasic 유틸리티 toorun 명령줄 또는 복사 파일에서 Xamarin, Android 및 기타 공급 업체에서 빌드를 호출 하 고 tooHockeyApp를 연결 하는 서비스가 있습니다.

![팀 서비스의 빌드 옵션](./media/iot-solution-build-system/image5.png)

### <a name="build-definitions"></a>빌드 정의
각각의 주요 대상 hello에 대 한 빌드 정의 해야합니다. 기능 및 회귀 테스트에 대한 변형이 있습니다. 다음이 제공됩니다.

* MyDriving.Services (hello 모바일 앱에 대 한 hello 백 엔드 웹 응용 프로그램)
* MyDriving.Xamarin.Android
  
  * MyDriving.Xamarin.Android-Feature
  * MyDriving.Xamarin.Android-Regression
* MyDriving.Xamarin.iOS
  
  * MyDriving.Xamarin.iOS-Feature
  * MyDriving.Xamarin.iOS-Regression
* MyDriving.Xamarin.UWP
  
  * MyDriving.Xamarin.UWP-Feature
  * MyDriving.Xamarin.UWP-Regression

이 구성의 toosee hello 전체 정보를 원하는 경우의 hello 4.7 섹션을 참조 [MyDriving 참조 가이드](http://aka.ms/mydrivingdocs), "빌드 및 릴리스 구성 합니다." Hello를 다음과 같은 일반적인 패턴입니다. hello 스크립트:

1. Hello NuGet 패키지를 복원합니다. 각 빌드의 hello 첫 번째 단계는 toorestore hello 필요한 NuGet 패키지 되므로 hello 리포지토리에 컴파일된 코드를 유지할 하지 있습니다.
2. Hello 라이선스를 활성화합니다. hello 빌드가 수행 되 hello 클라우드에서 라이선스-이 필요 하는 경우 특히, Xamarin 빌드 서비스-hello에 대 한 보도록 하겠습니다 tooactivate hello 현재 빌드 컴퓨터에서이 라이선스입니다. 그런 다음, 우리 비활성화 바로 다음에 tooallow 것 toobe 다른 컴퓨터에서 사용 합니다.
3. Hello 적절 한 서비스를 사용 하 여 빌드합니다. Xamarin 빌드 hello 모바일 앱에 대 한 사용 및 Visual Studio 빌드 hello 백 엔드 웹 서비스에 대 한 합니다.
4. 테스트를 작성합니다.
5. 테스트를 실행합니다. Xamarin 테스트 클라우드에서 hello 모바일 응용 프로그램 테스트를 실행 했습니다.
6. Hello 빌드 결과 toohello 저장 위치에 게시합니다.

hello 주 빌드에 대 한 hello 트리거 toocontinuous 통합을 설정 됩니다. 즉, hello 빌드 toohello 마스터 분기에 코드를 체크 될 때마다 실행 됩니다.

![여기서 hello 트리거는 집합 toocontinuous 통합 인터페이스](./media/iot-solution-build-system/image6.png)

### <a name="release-definitions"></a>릴리스 정의
릴리스 정의에서 설정 하는 많은 hello 동일한 방식으로 합니다.

Hello 웹 서비스에 대 한 Azure 웹 앱으로 배포를 설정합니다.

![Azure 웹앱으로 배포를 설정하기 위한 인터페이스](./media/iot-solution-build-system/image7.png)

및 hello 릴리스 트리거 toocontinuous 배포를 설정 하는 이유입니다. 즉, 모든 체크 인에 다음 업데이트 toohello web app에서 성공적인 빌드 결과입니다.

![Hello 릴리스 트리거 toocontinuous 배포 설정에 대 한 인터페이스](./media/iot-solution-build-system/image8.png)

모바일 앱에 대 한 tooHockeyApp 배포 했습니다.

![모바일 앱 tooHockeyApp를 배포 하기 위한 인터페이스](./media/iot-solution-build-system/image9.png)

## <a name="explore-telemetry-by-using-application-insights"></a>Application Insights를 사용하여 원격 분석 탐색
[Application Insights](../application-insights/app-insights-overview.md) hello 성능 및 웹 서비스의 사용에 대 한 원격 분석 수집 합니다. Application Insights SDK hello hello 서비스 toohello Azure에서 Application Insights 리소스에서에서 원격 분석을 보냅니다.

Toohello Application Insights 리소스를 설정 하는 해당 hello 서식 파일을 찾습니다. 여기의 hello 성능에 대 한 차트를 탐색할 수 있습니다 프로그램 [모바일 응용 프로그램 서비스 프로젝트](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileAppService)합니다. 서버 요청 및 응답 시간, 오류, 예외 수가 표시됩니다. 종속성 응답 시간-즉, 호출 toohello 데이터베이스와 tooREST 기계 학습 등 Api에 대 한 차트도 있습니다. 성능 문제가 경우 수 수 toosee 일으키는지 시스템의 어떤 부분을 수 있습니다.

![예제 성능 차트](./media/iot-solution-build-system/image11.png)

쉽게 tooget hello 동일한 차트를 직접 설정 하는 웹 서비스를 사용 하도록 설정한 경우. Hello 웹 서비스 블레이드에서 클릭 **도구** > **확장** > **추가**합니다. **Application Insights**를 선택합니다.

![Application Insights tooget hello 차트를 선택 하기 위한 인터페이스](./media/iot-solution-build-system/image12.png)

hello 기능은 hello Application Insights SDK로 응용 프로그램을 계측 하 여 작동 합니다.

사용자 지정 원격 분석 (또는 Azure 외부 위치에서 실행 되는 응용 프로그램 계측)를 추가할 수 있습니다 [Application Insights SDK hello 추가](../application-insights/app-insights-asp-net.md) 개발 시. 이 사용자의 평균 여행 길이 나 전체 주행 거리 같은 hello 응용 프로그램에 종속 된 유용한 toolog 메트릭을입니다. Visual Studio에서 hello 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 선택 **Application Insights 추가**합니다.

![Application Insights 추가 tooadd 사용자 지정 원격 분석을 선택 하기 위한 인터페이스](./media/iot-solution-build-system/image10.png)

Application Insights는 오류 응답 수가 비정상적인 것으로 나타나는 경우 경고 전자 메일을 보냅니다. 응답 시간과 같은 다양한 메트릭에 대한 사용자 고유의 알림을 설정할 수도 있습니다.

웹 서비스는 항상 최신 하 고 실행을 설정할 수 있습니다 정당한 toobe [가용성 테스트](../application-insights/app-insights-monitor-web-app-availability.md)합니다. 이러한 테스트는 15 분 마다 hello 전 세계 여러 위치에서 사이트를 ping합니다. 다시, toobe 문제가 결과적으로 하는 경우 전자 메일을 얻을 수 있습니다.

## <a name="estimate-operational-costs"></a>예상 운영 비용
되기 매우 저렴 한 toorun 작은 규모에 이와 같은 응용 프로그램. Hello 서비스 중 상당수가 추가 초급 무료 계층 개발 및 소규모 작업 비용 거의 됩니다. 및 앱 MyDriving에서 보여 주는 모든 hello 기능 toouse 물론 필요는 없습니다.

대략적인 예상 우리의 비용 MyDriving에 대 한 hello 개발 구성 설정에 다음과 같습니다. 또한 사용하지 *않았던* 몇 가지 다른 방법도 확인합니다. 이 정보는 자체 비용을 예측하므로 유용할 수 있습니다.

다음을 가정합니다.

* 5팀 이하(+ 이해 관계자 관찰)
* 약 한 달 동안 실행
* 하루에 네 개의 여정으로 100명의 사용자

> [!NOTE]
> 새 tooAzure 인 경우는 한 [무료 계정](https://azure.microsoft.com/free/)합니다.
> 
> 

| **서비스/구성 요소** | **참고 사항** | **비용/월** |
| --- | --- | --- |
| [Visual Studio 2015 Community](https://www.visualstudio.com/products/visual-studio-community-vs)와 [Xamarin](https://visualstudiogallery.msdn.microsoft.com/dcd5b7bd-48f0-4245-80b6-002d22ea6eee) <br/>플랫폼 간 개발 환경 |Visual Studio Community. (필요 [Visual Studio Professional](https://www.visualstudio.com/vs-2015-product-editions) 에 대 한 [Xamarin.Forms](https://xamarin.com/forms), 단일 코드 베이스에서 toodesign 플랫폼입니다.) |$0 |
| [Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/) <br/>양방향 데이터 연결 toodevices |8,000개 메시지 + 0.5KB/메시지 무료 |$0 |
| [Stream Analytics](https://azure.microsoft.com/pricing/details/stream-analytics/)  <br/>   고용량 스트림 데이터 처리 |사용된 동안 시간 및 스트리밍 단위당 $0.031 부과. Hello 스트리밍 단위 수입니다; 원하는 선택 더 많은 tooscale를 구성 합니다. |$23 |
| [기계 학습](https://azure.microsoft.com/documentation/services/machine-learning/)<br/> 적응 응답 |$10/사용자/월. <br/>                                                                                                                                                                                 + 3시간 테스트 \* $1/테스트 시간 <br/>                                                                                                                                                           + 3.5시간 API CPU \* $2/프로덕션 CPU 시간  <br/>                                                                                                                                                          API CPU 시간은 5분/일 재학습을 가정. 단, 입력 데이터가 많아지면 증가할 수 있음.                   <br/>                                                                                                                                                                     + 2 분/일 tooprocess 400 trips/일을 평가 합니다. |$20 |
| [App Service](https://azure.microsoft.com/pricing/details/app-service/)  <br/> 모바일 백 엔드에 대한 호스트 |B1 계층--프로덕션 웹앱 |$56 |
| [Visual Studio Team Services ](https://azure.microsoft.com/pricing/details/visual-studio-team-services/)  <br/> 빌드, 단위 테스트 및 릴리스 관리, 작업 관리 |사용자 에이전트, 5명의 사용자. |$0 |
| [Application Insights](https://azure.microsoft.com/pricing/details/application-insights/) <br/>웹 서비스 및 사이트의 성능 및 사용 현황 모니터링 |무료 계층. |$0 |
| [HockeyApp](http://hockeyapp.net/pricing/) <br/> 피드백, 사용 및 충돌 데이터의 컬렉션을 더한 베타 앱 배포 |새 사용자를 위한 두 가지 무료 앱.<br/> 이후에는 $30/월. |$0 |
| [Xamarin](https://store.xamarin.com/)<br/> 여러 장치에서 균일한 플랫폼에 대한 코드 |무료 평가판. <br/>이후에는 $25/월. |$0 |
| [SQL 데이터베이스](https://azure.microsoft.com/pricing/details/sql-database/)  |기본 계층, 단일 데이터베이스 모델. |$5 |
| [Service Fabric](https://azure.microsoft.com/pricing/details/service-fabric/)(선택 사항) |로컬 클러스터를 실행합니다. |$0 |
| [Power BI](https://powerbi.microsoft.com/pricing/)<br/> 스트리밍 및 정적 데이터에 대한 다양한 표시 및 조사 |무료 계층: 1GB, 10,000행/시간, 매일 새로 고침. <br/> [제한 확대](https://powerbi.microsoft.com/documentation/powerbi-power-bi-pro-content-what-is-it/), 추가 연결 옵션, 공동 작업을 위해 $10/사용자/월 |$0 |
| [저장소](https://azure.microsoft.com/pricing/details/storage/) |L(로컬 중복) &lt; 100 G$0.024/GB. |$3 |
| [데이터 팩터리](https://azure.microsoft.com/pricing/details/data-factory/) |활동당 $0.60 \* (8 - 5 FOC) |$2 |
| [HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/) <br/>  일일 재학습 |매일 1시간 동안 $0.32/시간으로 3개 A3 노드 * 31일. |$30 |
| [이벤트 허브](https://azure.microsoft.com/pricing/details/event-hubs/) |$11/월 처리량 단위(기본) + $0.028 수신. |$11 |
| OBD 동글 | |$12 |
| **합계** | |**$157** |

자세한 내용은 다음을 참조하세요.

* [Azure 서비스 할당량 및 제한](../azure-subscription-service-limits.md#iot-hub-limits)
* Azure [가격 계산기](https://azure.microsoft.com/pricing/calculator/)

## <a name="send-us-your-feedback"></a>사용자 의견을 보냅니다.
사용자 고유의 IoT 시스템 MyDriving toohelp 신속 작성 했기 때문에 얼마나 잘 작동 하는 방법에 대 한 사용자의 toohear 확실히 하려고 합니다. 다음의 경우 알려주세요.

* 문제 또는 도전 과제가 발생했습니다.
* 만들 때와 더 적합 한 tooyour 시나리오 있는 확장 지점이 있습니다.
* 특정 요구를 보다 효율적인 방식으로 tooaccomplish 찾을 있습니다.
* MyDriving 또는 이 설명서를 개선하기 위한 다른 제안이 있습니다.

toogive 사용자 의견 [문제 GitHub에서]를 제출 또는 아래 명령을 남길 (en-미국 버전).

의견에 귀 toohearing에서 있습니다!

## <a name="next-steps"></a>다음 단계
Hello 권장 [MyDriving 참조 가이드](http://aka.ms/mydrivingdocs), hello 디자인 hello 시스템 및 해당 구성 요소에 대 한 포괄적인 설명은 변수인 합니다.

