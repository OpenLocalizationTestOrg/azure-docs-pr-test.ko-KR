---
title: "Xamarin.Forms를 사용 하 여 aaaGet 모바일 앱 시작"
description: "Xamarin.Forms 개발에 대 한 모바일 앱을 사용 하 여이 자습서 toostart를 수행 합니다."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 5e692220-cc89-4548-96c8-35259722acf5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: af6b1c1ce4cf91c397552aa3d8ee40728129238c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinforms-app"></a>Xamarin.Forms 앱 만들기
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>개요
이 자습서를 사용 하 여 클라우드 기반 백 엔드 서비스 tooa Xamarin.Forms 모바일 앱 tooadd hello 백 엔드 Azure 앱 서비스 모바일 앱 기능 hello 하는 방법을 보여 줍니다. 새 Mobile Apps 백 엔드와 앱 데이터를 Azure에 저장하는 간단한 할 일 모음 Xamarin.Forms 앱을 만듭니다.

이 자습서를 완료해야 다른 모든 Xamarin.Forms용 모바일 앱 자습서를 진행할 수 있습니다.

## <a name="prerequisites"></a>필수 조건
toocomplete이이 자습서에서는 다음 hello 필요:

* 활성 Azure 계정. 계정이 없는, Azure 평가판에 등록할 수 있으며 too10 가능한 모바일 앱을 계속 사용할 수 있습니다 프로그램 평가 종료 후에 준비. 자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.

* Xamarin이 포함된 Visual Studio입니다. 내용은 hello를 참조 하십시오. [설정 및 Visual Studio 및 Xamarin이 설치](https://msdn.microsoft.com/library/mt613162.aspx) 페이지.

* Xcode v7.0 이상 및 Xamarin Studio Community가 설치된 Mac입니다. 자세한 내용은 [Visual Studio 및 Xamarin을 위한 설정 및 설치](https://msdn.microsoft.com/library/mt613162.aspx) 및 [Mac 사용자를 위한 설정, 설치 및 확인](https://msdn.microsoft.com/library/mt488770.aspx)(MSDN)을 참조하세요.

## <a name="create-a-new-mobile-apps-back-end"></a>새 Mobile Apps 백 엔드 만들기

다시 한 새로운 모바일 앱을 종료 toocreate 다음 hello지 않습니다.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

이제 모바일 클라이언트 응용 프로그램에서 사용할 수 있는 Mobile Apps 백 엔드를 설정했습니다. 다음으로 간단한 할 일 목록 백 엔드에 대 한 서버 프로젝트를 다운로드 하 고 tooAzure 게시 합니다.

## <a name="configure-hello-server-project"></a>Hello 서버 프로젝트를 구성 합니다.

tooconfigure hello 서버 프로젝트 toouse Node.js 또는.NET 백 엔드 hello 중 하나, 다음 hello지 않습니다.

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinforms-solution"></a>다운로드 하 고 hello Xamarin.Forms 솔루션 실행

두 가지 방법 중 하나로 hello 솔루션을 다운로드할 수 있습니다. Mac tooa 다운로드 하 고 Xamarin Studio에서 엽니다 다운로드 tooa Windows 컴퓨터 한 hello iOS 앱을 작성 하기 위한 네트워크로 연결 된 Mac을 사용 하 여 Visual Studio에서 엽니다. 자세한 내용은 [Visual Studio 및 Xamarin 설정 및 설치](https://msdn.microsoft.com/library/mt613162.aspx)를 참조하세요.

Windows 또는 Mac 컴퓨터에서 수행 hello 다음:

1. Toohello 이동 [Azure 포털]합니다.

2. Hello에 **설정** 블레이드 모바일 앱에 대 한 아래 **모바일**선택, **시작** > **Xamarin.Forms**합니다. **3단계** 아래에서 **새 앱 만들기**를 선택한 후 **다운로드**를 선택합니다.

   이 작업은 연결 된 tooyour 모바일 앱 하는 클라이언트 응용 프로그램을 포함 하는 프로젝트를 다운로드 합니다. Hello 압축 된 프로젝트 파일 tooyour 로컬 컴퓨터를 저장 하 고 저장할 위치를 메모 합니다.

3. Hello 프로젝트 다운로드 한 압축을 풀고 Visual Studio (Windows) 또는 Xamarin Studio (Mac)에서 엽니다.

   ![Xamarin Studio에서 추출된 프로젝트][9]

   ![Visual Studio에서 추출된 프로젝트][8]

## <a name="optional-run-hello-ios-project"></a>(선택 사항) Hello iOS 프로젝트를 실행 합니다.
이 섹션에서는 iOS 장치에 대 한 hello Xamarin iOS 프로젝트를 실행합니다. iOS 장치를 작업하지 않는 경우 이 섹션을 건너뛸 수 있습니다.

#### <a name="in-xamarin-studio"></a>Xamarin Studio에서
1. Hello iOS 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 선택 **시작 프로젝트로 설정**합니다.

2. Hello에 **실행** 메뉴 선택 **디버깅 시작** toobuild 프로젝트 hello 및 hello iPhone 에뮬레이터의 hello 응용 프로그램을 시작 합니다.

#### <a name="in-visual-studio"></a>Visual Studio에서
1. Hello iOS 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 선택 **시작 프로젝트로 설정**합니다.

2. Hello에 **빌드** 메뉴 선택 **Configuration Manager**합니다.

3. Hello에 **Configuration Manager** 대화 상자, 선택 hello **빌드** 및 **배포** 확인란 다음 toohello iOS 프로젝트.

4. toobuild 프로젝트 hello 및 선택 hello hello iPhone 에뮬레이터의 hello 응용 프로그램을 시작 **F5** 키입니다.

   > [!NOTE]
   > Hello 프로젝트를 구축 하는 데 문제가 있으면 hello NuGet 패키지 관리자 및 update toohello 최신 버전의 hello Xamarin 지원 패키지를 실행 합니다. 퀵 스타트 프로젝트 느린 tooupdate toohello 최신 버전을 수 있습니다.    
   >
   >

5. Hello 앱 의미 있는 텍스트를 같은 입력 *알아보려면 Xamarin*, 한 다음 선택 hello 더하기 기호 (**+**).

    ![][10]

    이 작업에는 새 모바일 앱 백 엔드 Azure에서 호스팅되는 post 요청 toohello를 보냅니다. Hello 요청에서 데이터는 hello TodoItem 테이블에 삽입 됩니다. Hello 테이블에 저장 된 항목을 데이터 hello 목록에 표시 되며 다시 모바일 앱을 종료 하 고 hello hello 반환 됩니다.

    > [!NOTE]
    > 모바일 앱 백 엔드 hello TodoItemManager.cs C# 솔루션의 hello 이식 가능한 클래스 라이브러리 프로젝트의 파일에에서 액세스 하는 hello 코드를 찾을 수 있습니다.
    >
    >

## <a name="optional-run-hello-android-project"></a>(선택 사항) Hello Android 프로젝트를 실행 합니다.
이 섹션에서는 Android 용 hello Xamarin 로봇 프로젝트를 실행합니다. Android 장치를 작업하지 않는 경우 이 섹션을 건너뛸 수 있습니다.

#### <a name="in-xamarin-studio"></a>Xamarin Studio에서

1. Hello Android 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 선택 **시작 프로젝트로 설정**합니다.

2. toobuild 프로젝트 hello 및 hello에 Android 에뮬레이터의 hello 응용 프로그램을 시작 **실행** 메뉴 선택 **디버깅 시작**합니다.

#### <a name="in-visual-studio"></a>Visual Studio에서

1. Hello (로봇) Android 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 선택 **시작 프로젝트로 설정**합니다.

2. Hello에 **빌드** 메뉴 선택 **Configuration Manager**합니다.

3. Hello에 **Configuration Manager** 대화 상자, 선택 hello **빌드** 및 **배포** 확인란 다음 toohello Android 프로젝트입니다.

4. toobuild 프로젝트 hello 및 선택 hello Android 에뮬레이터의 hello 응용 프로그램을 시작 **F5** 키입니다.

   > [!NOTE]
   > Hello 프로젝트를 구축 하는 데 문제가 있으면 hello NuGet 패키지 관리자 및 update toohello 최신 버전의 hello Xamarin 지원 패키지를 실행 합니다. 퀵 스타트 프로젝트 느린 tooupdate toohello 최신 버전을 수 있습니다.    
   >
   >

5. Hello 앱 의미 있는 텍스트를 같은 입력 *알아보려면 Xamarin*, 한 다음 선택 hello 더하기 기호 (**+**).

    ![][11]
    
    이 작업에는 새 모바일 앱 백 엔드 Azure에서 호스팅되는 post 요청 toohello를 보냅니다. Hello 요청에서 데이터는 hello TodoItem 테이블에 삽입 됩니다. Hello 테이블에 저장 된 항목을 데이터 hello 목록에 표시 되며 다시 모바일 앱을 종료 하 고 hello hello 반환 됩니다.
    
    > [!NOTE]
    > 모바일 앱 백 엔드 hello TodoItemManager.cs C# 솔루션의 hello 이식 가능한 클래스 라이브러리 프로젝트의 파일에에서 액세스 하는 hello 코드를 찾을 수 있습니다.
    >
    >

## <a name="optional-run-hello-windows-project"></a>(선택 사항) Hello Windows 프로젝트를 실행 합니다.

이 섹션에서는 Windows 장치에 대 한 Xamarin WinApp 프로젝트 hello를 실행합니다. Windows 장치를 작업하지 않는 경우 이 섹션을 건너뛸 수 있습니다.

#### <a name="in-visual-studio"></a>Visual Studio에서

1. Hello Windows 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 선택 **시작 프로젝트로 설정**합니다.

2. Hello에 **빌드** 메뉴 선택 **Configuration Manager**합니다.

3. Hello에 **Configuration Manager** 대화 상자, 선택 hello **빌드** 및 **배포** 확인란 다음 toohello Windows 프로젝트를 선택 합니다.

4. toobuild 프로젝트 hello 및 선택 hello Windows 에뮬레이터의 hello 응용 프로그램을 시작 **F5** 키입니다.

   > [!NOTE]
   > Hello 프로젝트를 구축 하는 데 문제가 있으면 hello NuGet 패키지 관리자 및 update toohello 최신 버전의 hello Xamarin 지원 패키지를 실행 합니다. 퀵 스타트 프로젝트 느린 tooupdate toohello 최신 버전을 수 있습니다.    
   >
   >

5. Hello 앱 의미 있는 텍스트를 같은 입력 *알아보려면 Xamarin*, 한 다음 선택 hello 더하기 기호 (**+**).

    이 작업에는 새 모바일 앱 백 엔드 Azure에서 호스팅되는 post 요청 toohello를 보냅니다. Hello 요청에서 데이터는 hello TodoItem 테이블에 삽입 됩니다. Hello 테이블에 저장 된 항목을 데이터 hello 목록에 표시 되며 다시 모바일 앱을 종료 하 고 hello hello 반환 됩니다.
    
    ![][12]
    
    > [!NOTE]
    > 모바일 앱 백 엔드 hello TodoItemManager.cs C# 솔루션의 hello 이식 가능한 클래스 라이브러리 프로젝트의 파일에에서 액세스 하는 hello 코드를 찾을 수 있습니다.
    >
    >

## <a name="next-steps"></a>다음 단계

* [인증 tooyour 앱 추가](app-service-mobile-xamarin-forms-get-started-users.md)  
  자세한 내용은 방법 tooauthenticate 사용자가 id 공급자로 사용 하 여 앱의 합니다.

* [푸시 알림 tooyour 앱 추가](app-service-mobile-xamarin-forms-get-started-push.md)  
  Tooadd 푸시 알림을 tooyour 앱을 지원 하는 방법을 알아보고 모바일 앱 백 엔드 toouse Azure 알림 허브 toosend hello 푸시 알림을 구성 합니다.

* [앱에 오프라인 동기화 사용](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  자세한 방법을 모바일 앱을 사용 하 여 앱에 대 한 오프 라인 지원 tooadd 백 엔드 합니다. 오프라인 동기화를 사용하면 네트워크에 연결되어 있지 않은 경우에도 모바일 앱의 데이터를 보거나, 추가하거나, 수정할 수 있습니다.

* [모바일 앱에 대 한 관리 되는 클라이언트 hello를 사용 하 여](app-service-mobile-dotnet-how-to-use-client-library.md)  
  Hello로 toowork SDK Xamarin 앱에 클라이언트를 관리 하는 방법을 알아봅니다.

<!-- Anchors. -->
[Get started with Mobile Apps back ends]:#getting-started
[Create a new Mobile Apps back end]:#create-new-service
[Next steps]:#next-steps


<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart.png
[8]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-vs.png
[9]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-xs.png
[10]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-ios.png
[11]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-android.png
[12]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-windows.png


<!-- URLs. -->
[Visual Studio Professional 2013]: https://go.microsoft.com/fwLink/p/?LinkID=257546
[Mobile app SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure 포털]: https://portal.azure.com/
