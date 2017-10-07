---
title: "Xamarin.Android 앱에 대 한 aaaGet Azure 모바일 앱 시작"
description: "Azure 모바일 앱을 사용 하 여 Xamarin Android 개발을 위한 시작 자습서 tooget이를 수행 합니다."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 81649dd3-544f-40ff-b9b7-60c66d683e60
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 38710660d9328fe3c068efca972f76aa8b6e049b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinandroid-app"></a>Xamarin.Android 앱 만들기
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>개요
이 자습서에서는 tooadd 클라우드 기반 백 엔드 tooa Xamarin.Android 응용 프로그램을 서비스 하는 방법을 보여 줍니다. 자세한 내용은 [모바일 앱 정의](app-service-mobile-value-prop.md)를 참조하세요.

완료 하는 hello 앱의 스크린 샷을 다음과 같습니다.

![][0]

이 자습서를 완료해야 다른 모든 Xamarin Android 앱용 모바일 앱 자습서를 진행할 수 있습니다.

## <a name="prerequisites"></a>필수 조건
toocomplete이이 자습서에서는 다음 필수 구성 요소는 hello 필요:

* 활성 Azure 계정. 계정이 없는, Azure 평가판에 등록 및 too10 무료 모바일 앱을 준비 합니다. 자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.
* Xamarin이 포함된 Visual Studio입니다. 지침은 [Visual Studio 및 Xamarin을 위한 설치 및 설정](https://msdn.microsoft.com/library/mt613162.aspx) 을 참조하세요.

## <a name="create-an-azure-mobile-app-backend"></a>새 Azure Mobile App 백 엔드 만들기
이러한 단계 toocreate 모바일 앱 백 엔드를 따릅니다.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

이제 모바일 클라이언트 응용 프로그램에서 사용할 수 있는 Azure 모바일 앱 백 엔드를 프로비저닝했습니다. 다음으로 간단한 "할 일 목록"에 대 한 서버 프로젝트를 다운로드 백 엔드 tooAzure 게시 합니다.

## <a name="configure-hello-server-project"></a>Hello 서버 프로젝트를 구성 합니다.
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinandroid-app"></a>다운로드 하 고 hello Xamarin.Android 앱 실행
1. **다운로드 하 고 Xamarin.Android 프로젝트 실행**, hello 클릭 **다운로드** 단추입니다.

      Hello 압축 된 프로젝트 파일 tooyour 로컬 컴퓨터를 저장 하 고 저장할 위치를 메모 합니다.
2. 키를 눌러 hello **F5** toobuild hello 프로젝트 키 및 hello 응용 프로그램을 시작 합니다.
3. Hello 앱 의미 있는 텍스트를 같은 입력 *완료 hello 자습서* hello를 클릭 한 다음 **추가** 단추입니다.

    ![][10]

    Hello 요청에서 데이터는 hello TodoItem 테이블에 삽입 됩니다. Hello 테이블에 저장 된 항목 hello 모바일 앱 백엔드에서 돌아와 hello 목록에 데이터가 나타납니다.

   > [!NOTE]
   > 모바일 앱 백 엔드 tooquery에 액세스 하는 hello 코드를 검토할 수 있으며 hello ToDoActivity.cs C# 파일에에서 있는 데이터를 삽입할 수 있습니다.
   >
   >

## <a name="next-steps"></a>다음 단계
* [오프 라인 동기화 tooyour 앱 추가](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [인증 tooyour 앱 추가](app-service-mobile-xamarin-android-get-started-users.md)
* [푸시 알림 tooyour Xamarin.Android 앱 추가](app-service-mobile-xamarin-android-get-started-push.md)
* [Toouse hello Azure 모바일 앱에 대 한 클라이언트를 관리 하는 방법](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
