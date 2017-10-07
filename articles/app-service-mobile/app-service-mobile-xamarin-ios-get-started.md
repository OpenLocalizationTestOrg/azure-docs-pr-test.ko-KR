---
title: "Xamarin.iOS 앱 용 Azure 앱 서비스 모바일 앱 시작 aaaGet | Microsoft Docs"
description: "이 자습서 tooget Xamarin.iOS 개발에 대 한 모바일 앱을 사용 하 여 시작을 수행 합니다."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 14428794-52ad-4b51-956c-deb296cafa34
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: syntaxc4
ms.openlocfilehash: 524c5ac4d8a29d7cb858f74132aad5d6e2201d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinios-app"></a>Xamarin.iOS 앱 만들기
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>개요
이 자습서는 Azure 모바일 앱 백 엔드를 사용 하 여 클라우드 기반 백 엔드 tooadd tooa Xamarin.iOS 모바일 앱 서비스 하는 방법을 보여 줍니다.  새 모바일 앱 백 엔드와 앱 데이터를 Azure에 저장하는 간단한 *할 일 모음* Xamarin.iOS 앱을 만듭니다.

Azure 앱 서비스의 hello 모바일 앱 기능을 사용 하는 방법에 대 한 다른 모든 Xamarin.iOS 자습서에 대 한 필수 구성 요소는이 자습서를 완료 합니다.

## <a name="prerequisites"></a>필수 조건
toocomplete이이 자습서에서는 다음 필수 구성 요소는 hello 필요:

* 활성 Azure 계정. 계정이 없으면 Azure 평가판에 등록 하 고 too10 가능한 모바일 앱을 계속 사용할 수 있습니다 프로그램 평가 종료 후에 작동 합니다. 자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.
* Xamarin이 포함된 Visual Studio입니다. 지침은 [Visual Studio 및 Xamarin을 위한 설치 및 설정](https://msdn.microsoft.com/library/mt613162.aspx) 을 참조하세요.
* Xcode v7.0 이상 및 Xamarin Studio Community가 설치된 Mac입니다. [Visual Studio 및 Xamarin을 위한 설정 및 설치](https://msdn.microsoft.com/library/mt613162.aspx) 및 [Mac 사용자를 위한 설정, 설치 및 유효성 검사](https://msdn.microsoft.com/library/mt488770.aspx)(MSDN)를 참조하세요.

## <a name="create-an-azure-mobile-app-backend"></a>새 Azure Mobile App 백 엔드 만들기
이러한 단계 toocreate 모바일 앱 백 엔드를 따릅니다.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a>Hello 서버 프로젝트를 구성 합니다.
이제 모바일 클라이언트 응용 프로그램에서 사용할 수 있는 Azure 모바일 앱 백 엔드를 프로비저닝했습니다. 다음으로 간단한 "할 일 목록"에 대 한 서버 프로젝트를 다운로드 백 엔드 tooAzure 게시 합니다.

다음 단계 tooconfigure hello 서버 프로젝트 toouse hello 어느 hello Node.js 또는.NET 백 엔드를 따릅니다.

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinios-app"></a>다운로드 하 고 hello Xamarin.iOS 앱 실행
1. 열기 hello [Azure 포털] 브라우저 창에서.
2. 모바일 앱에 대 한 hello 설정 블레이드에서 클릭 **시작** > **Xamarin.iOS**합니다. 3단계 아래에서 **새 앱 만들기** 가 선택되어 있지 않으면 클릭합니다.  그런 다음 hello 클릭 **다운로드** 단추입니다.

      Tooyour 모바일 백 엔드를 연결 하는 클라이언트 응용 프로그램 다운로드 됩니다. 로컬 컴퓨터에 hello 압축 된 프로젝트 파일을 저장 하 고 저장할 위치를 메모 합니다.
3. Hello 프로젝트 다운로드 한 압축을 풀고 Xamarin Studio (또는 Visual Studio)에서 엽니다.

    ![][9]

    ![][8]
4. Hello F5 키 toobuild hello 프로젝트를 누르고 hello iPhone 에뮬레이터의 hello 응용 프로그램을 시작 합니다.
5. Hello 앱 의미 있는 텍스트를 같은 입력 *알아보려면 Xamarin*, hello를 클릭 한 다음  **+**  단추입니다.

    ![][10]

    Hello 요청에서 데이터는 hello TodoItem 테이블에 삽입 됩니다. Hello 테이블에 저장 된 항목 hello 모바일 앱 백엔드에서 돌아가고 데이터가 hello 목록에 표시 됩니다.

> [!NOTE]
> 모바일 앱 백 엔드 tooquery에 액세스 하는 hello 코드를 검토할 수 있으며 hello QSTodoService.cs C# 파일에에서 데이터를 삽입할 수 있습니다.
>
>

## <a name="next-steps"></a>다음 단계
* [오프 라인 동기화 tooyour 앱 추가](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [인증 tooyour 앱 추가](app-service-mobile-xamarin-ios-get-started-users.md)
* [푸시 알림 tooyour Xamarin.Android 앱 추가](app-service-mobile-xamarin-ios-get-started-push.md)
* [Toouse hello Azure 모바일 앱에 대 한 클라이언트를 관리 하는 방법](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Anchors. -->
[Getting started with mobile app backends]:#getting-started
[Create a new mobile app backend]:#create-new-service
[Next Steps]:#next-steps

<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-ios-get-started/xamarin-ios-quickstart.png
[8]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-vs.png
[9]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-xs.png
[10]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-quickstart-startup-ios.png

<!-- URLs. -->
[Azure 포털]: https://portal.azure.com/
