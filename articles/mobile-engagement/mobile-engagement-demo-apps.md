---
title: "Mobile Engagement 데모 앱의 aaaAzure | Microsoft Docs"
description: "위치를 설명 toodownload, 어떻게 toouse, 및 hello 이점은 Azure Mobile Engagement 응용 프로그램 데모"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: f624d5aa-254b-4ad0-96a3-f00e6c3a2c97
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2016
ms.author: piyushjo
ms.openlocfilehash: 9ff0df0d21e1bad6aff573db49304a55593df1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-demo-app"></a>Azure Mobile Engagement 데모 앱
에 대 한 Azure Mobile Engagement 데모 응용 프로그램 게시 했습니다 **iOS**, **Android**, 및 **Windows** 플랫폼 toohelp 있습니다 toofind 유용한 리소스 및 Mobile에 대 한 자세한 정보 계약에 서명입니다.

hello 앱을 사용 하면 수 있습니다.

* 유용한 링크 tooMobile 비디오, 설명서, hello 지원 포럼와 같은 리소스를 쉽게 찾을 toogo tooraise 기능을 요청 합니다.
* 사용자의 모바일 응용 프로그램에 대 한 tooget 아이디어 Mobile Engagement에서 지 원하는 환경 샘플 알림입니다.
* 참조 구현 toostudy를 어떻게 사용 하 여 사용자 고유의 응용 프로그램에 Mobile Engagement tooimplement 합니다. 다음을 배울 수 있습니다.
  
  * 분석 데이터 수집
  * *전체 화면 중간* 또는 *팝업*과 같은 형식의 고급 알림 시나리오 구현
  * 설문 조사 구현
  * 자동 푸시 데이터 및 푸시 시나리오 구현   

## <a name="app-installation"></a>앱 설치
이 앱은 hello 다음 앱 스토어에서에서 사용할 수 있습니다.

* **Windows 유니버설 데모 앱**:
  
  * Hello에 hello 앱을 다운로드 [Windows 앱 스토어](https://www.microsoft.com/en-us/store/apps/azure-mobile-engagement/9nblggh4qmh2)합니다.
  * hello 앱은 Windows 10 유니버설 앱으로 개발 되었습니다. hello 소스 코드에서 사용할 수는 [GitHub](https://github.com/Azure/azure-mobile-engagement-app-windows)합니다.
* **iOS 데모 앱**:
  
  * Hello에 hello 앱을 다운로드 [Apple 스토어](https://itunes.apple.com/us/app/azure%20mobile%20engagement/id1105090090)합니다.
  * iOS Swift hello 앱 개발 되었습니다. hello 소스 코드에서 사용할 수는 [GitHub](https://github.com/Azure/azure-mobile-engagement-app-ios)합니다.
* **Android 데모 앱**:
  
  * Hello에 hello 앱을 다운로드 [Google Play 스토어](https://play.google.com/store/apps/details?id=com.microsoft.azure.engagement)합니다.
  * hello 소스 코드에서 사용할 수는 [GitHub](https://github.com/Azure/azure-mobile-engagement-app-android)합니다.

![Windows 유니버설 데모 앱][1]

![iOS 데모 앱][2]
![Android 데모 앱][3]

## <a name="usage"></a>사용
다음 방법으로 hello에이 앱을 사용할 수 있습니다.

**장치에서 앱 hello hello (이전 제공 됨)는 응용 프로그램 스토어 링크에서 다운로드:**

> [!IMPORTANT]
> Azure 계정이 필요 하지 않습니다 또는 tooconnect hello 앱 tooa 백 엔드 필요 합니다. hello 앱 독립적으로 작동합니다.
> 
> 

* 장치에서 hello 앱을 설정한 후에 hello 왼쪽 메뉴 toofind hello 유용한 리소스에서 Mobile Engagement에 대 한 hello 링크를 통해 이동할 수 있습니다.
* Hello 추가한 [서비스의 RSS 피드](https://aka.ms/azmerssfeed) 이 응용 프로그램에 항상 hello 최신 제품 업데이트에 대 한 업데이트 되도록 합니다.
* Hello 샘플 알림 시나리오 tooexperience hello 유형의 지원 되는 Mobile Engagement에서 각 플랫폼에 대 한 알림을 통해 이동할 수 있습니다. 이러한 알림을 수 hello Mobile Engagement 플랫폼에서 동일한 toosending hello 알림을 알림 경험을 hello 로컬로-즉, 클릭할 수 있는 hello 단추 hello 화면 tooshow에 숙련 된 합니다.

![Windows용 앱 메뉴][4]

![iOS용 앱 메뉴][5]
![Android용 앱 메뉴][6]

**Hello GitHub (제공 된 링크 앞)에서 hello 소스 코드를 다운로드 하세요.**

* Hello 소스 코드를 다운로드 한 후 hello 각각의 개발 환경-iOS, Android 및 Windows 용 Visual Studio에 대 한 Android Studio 용 XCode에서에서 엽니다.
* 다음을 따라야 우리의 [기본 SDK 통합 단계](mobile-engagement-windows-store-dotnet-get-started.md) 이 응용 프로그램 tooits Mobile Engagement 백 엔드 인스턴스를 소유 tooconnect 수 없도록 합니다.
  * Tooconfigure hello 응용 프로그램에서 연결 문자열을 해야합니다.
  * 또한 해야 tooconfigure hello 푸시 알림 플랫폼 앱에 대 한 합니다.
* Mobile Engagement와 해당 hello 앱 자체 계측을 확인할 수 있습니다. 따라서 hello 앱 백 엔드 toohello 연결한 후를 열 수 없게 toosee hello 사용자 세션, 활동, 이벤트 및 hello에서 이런 식으로 **모니터** 탭 합니다.
* 또한 로컬 알림을 사용 하는 대신 사용자 고유의 Mobile Engagement 인스턴스에서 수 toosend 알림 toothis 앱 수 수 있습니다.
  
  * Hello를 사용 하 여 테스트 장치도 장치를 추가할 수는 여기 **Get hello 장치 ID** hello 응용 프로그램에서 메뉴 항목입니다. 그러면 플랫폼 백 엔드 인스턴스를 사용하여 테스트 장치로 등록할 수 있는 장치 ID가 제공됩니다.
    
    ![Windows의 장치 ID][7]
    
    ![iOS의 장치 ID][8]
    ![Android의 장치 ID][9]

## <a name="key-features-of-hello-demo-app"></a>Hello 데모 응용 프로그램의 주요 기능
* 에서 설명한 대로이 앱에 있는 모든 hello 주요 리소스 Mobile Engagement에 대 한 손 합니다. Hello 왼쪽된 메뉴에서 hello 링크를 통해 이동할 수 있습니다.
* 각 플랫폼에 대한 앱 알림을 경험할 수 있습니다. 이러한 알림을으로 배달할 수 **알림 전용**여기서 hello 알림을 클릭을 열면 hello 응용 프로그램의 네이티브 화면, (사용 하 여 **직접 링크**)-또는 **웹 알림**, 위치를 제공할 수 있습니다 추가 HTML 콘텐츠 Mobile Engagement 다시 종료 hello에서 toobe hello 알림을 클릭할 때 표시 됩니다.
  
    ![앱 알림][29]
* Ios, tooclose hello 앱 toosee hello 앱 아웃 또는 시스템 푸시 알림을 해야합니다. Hello 여기 구현을 추가 하는 데 볼 수 있습니다 **실행 단추**추가 toothis에 대 한 응용 프로그램의 알림은 hello 같이 *피드백* 및 *공유* ( hello 사용자가 수행할 수 hello 알림 자체에서 작업 바로).
  
    ![iOS의 앱 알림][11] ![iOS의 앱 알림 표시][14]
* Android에서는 hello는 지원 옵션을 추가 하는 여러 줄 텍스트 (**큰 텍스트**) 또는 알림 이미지 (**큰 그림**) hello 함께 toohello 알림 **실행단추** (에서 지 원하는 대로 iOS).
  
    ![Android의 앱 알림][12] ![Android의 앱 알림 표시][15]
* Windows 10 PC hello에 나타나는 모양을 hello 알림을 볼 수 있습니다. 이 알림은에 표시 hello Windows 10 **알림 센터**합니다. 추가 대 한 지원은 **실행 단추** hello 시점 hello Windows SDK에서에서 합니다.
  
    ![Windows의 앱 알림][10] ![Windows의 앱 표시][13]
* 각 플랫폼의 기본 "앱 내" 알림을 경험할 수 있습니다. **알림** 창이 먼저 표시되는 2단계 환경입니다. 전체 화면을 엽니다 클릭 하면 **알림**hello 스크린 샷 뒤에 표시 된 대로, 합니다. 이 발표의 hello 내용은 Mobile Engagement 백 엔드 인스턴스에서 가져옵니다. SDK hello 알림과 공지에 대 한 hello 서식 파일에 있습니다. 쉽게 사용자 지정할 수 있습니다, hello 추가 우리의 로고와 색 지정 된 사용이 데모 응용 프로그램에 표시 된 대로 합니다.  
  
    ![Windows의 앱 내 알림][16]
  
    ![iOS의 앱 내 알림][17]  ![Android의 앱 내 알림][18]
  
    **iOS**, **Android**
* Hello를 사용할 수도 있습니다 **범주** Mobile Engagement toocustomize의 기능이 기본 환경입니다. Hello 데모 응용 프로그램에서 두 가지 일반적인 방법으로 toochange hello 경험 hello 알림의 시연을 했습니다. Note hello 범주 기능 hello Windows SDK에서에서 아직 지원 되지 않습니다.
  
    **전체 화면 중간:**
  
    ![앱 내 알림 - 중간 범주][30]
  
    ![iOS의 중간 범주][21]     ![Android의 중간 범주][22]
  
    **팝업 알림:**
  
    ![앱 내 알림 - 팝업 범주][31]
  
    ![iOS의 팝업 알림][19]    ![Android의 팝업 알림][20]

**iOS**, **Android**

* Mobile Engagement는 **설문 조사**라는 전문 앱 내 알림도 지원합니다. 이렇게 하면 toosend 빠른 설문 조사 tooyour 분할 응용 프로그램 사용자가 있습니다. 질문 및 hello 다음 스크린 샷에서 같이 각 질문에 대 한 옵션을 추가할 수 있습니다. 이 앱에서 알림 toohello 응용 프로그램 사용자로 표시 다음 됩니다.   
  
    ![설문 조사 알림][32]
  
    ![Windows의 설문 조사][26]
  
    ![iOS의 설문 조사][27]   ![Android의 설문 조사][28]

**iOS**, **Android**

* Mobile Engagement는 자동 **데이터 푸시** 알림도 전송할 수 있습니다. 이러한 알림 (예: hello JSON 데이터의 다음 예제는 hello)를 서비스에서 데이터를 보낼 수 있는 응용 프로그램에서 처리 하 고 몇 가지 조치를 취할 수 있습니다. 예 어떻게이 예에서는 변경 항목의 hello 가격 선택적으로 데이터 푸시 알림을 사용 하 여입니다.
  
    ![데이터 푸시 알림][33]
  
    ![Windows의 데이터 푸시 알림][23]
  
    ![iOS의 데이터 푸시 알림][24]  ![Android의 데이터 푸시 알림][25]

**iOS**, **Android**

> [!NOTE]
> 클릭 하 여 이러한 알림을 중 하나에 대 한 자세한 단계별 지침을 볼 수 있습니다 **여기를 클릭 하는 방법에 대 한 지침은 toosend Mobile Engagement 플랫폼에서 이러한 알림을** 샘플 알림 화면에서 합니다.
> 
> 

[1]: ./media/mobile-engagement-demo-apps/home-windows.png
[2]: ./media/mobile-engagement-demo-apps/home-ios.png
[3]: ./media/mobile-engagement-demo-apps/home-android.png
[4]: ./media/mobile-engagement-demo-apps/menu-windows.png
[5]: ./media/mobile-engagement-demo-apps/menu-ios.png
[6]: ./media/mobile-engagement-demo-apps/menu-android.png
[7]: ./media/mobile-engagement-demo-apps/device-id-windows.png
[8]: ./media/mobile-engagement-demo-apps/device-id-ios.png
[9]: ./media/mobile-engagement-demo-apps/device-id-android.png
[10]: ./media/mobile-engagement-demo-apps/out-of-app-windows.png
[11]: ./media/mobile-engagement-demo-apps/out-of-app-ios.png
[12]: ./media/mobile-engagement-demo-apps/out-of-app-android.png
[13]: ./media/mobile-engagement-demo-apps/out-of-app-display-windows.png
[14]: ./media/mobile-engagement-demo-apps/out-of-app-display-ios.png
[15]: ./media/mobile-engagement-demo-apps/out-of-app-display-android.png
[16]: ./media/mobile-engagement-demo-apps/in-app-windows.png
[17]: ./media/mobile-engagement-demo-apps/in-app-ios.png
[18]: ./media/mobile-engagement-demo-apps/in-app-android.png
[19]: ./media/mobile-engagement-demo-apps/pop-up-ios.png
[20]: ./media/mobile-engagement-demo-apps/pop-up-android.png
[21]: ./media/mobile-engagement-demo-apps/interstitial-ios.png
[22]: ./media/mobile-engagement-demo-apps/interstitial-android.png
[23]: ./media/mobile-engagement-demo-apps/data-push-windows.png
[24]: ./media/mobile-engagement-demo-apps/data-push-ios.png
[25]: ./media/mobile-engagement-demo-apps/data-push-android.png
[26]: ./media/mobile-engagement-demo-apps/survey-windows.png
[27]: ./media/mobile-engagement-demo-apps/survey-ios.png
[28]: ./media/mobile-engagement-demo-apps/survey-android.png
[29]: ./media/mobile-engagement-demo-apps/out-of-app.png
[30]: ./media/mobile-engagement-demo-apps/in-app-interstitial.png
[31]: ./media/mobile-engagement-demo-apps/in-app-pop-up.png
[32]: ./media/mobile-engagement-demo-apps/notification-poll.png
[33]: ./media/mobile-engagement-demo-apps/notification-data-push.png
