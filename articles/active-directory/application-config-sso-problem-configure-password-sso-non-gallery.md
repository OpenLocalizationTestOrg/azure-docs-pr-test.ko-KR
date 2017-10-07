---
title: "aaaProblem 암호 single sign on 갤러리가 아닌 응용 프로그램에 대 한 구성 | Microsoft Docs"
description: "암호 Single sign-on 나열 되지 않은 사용자 지정 갤러리 아닌 응용 프로그램에 대 한 hello Azure AD 응용 프로그램 갤러리에서에서 구성할 때 일반적인 문제 사람이 면 hello 이해"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 3aee0a4c525bb3da338da2da0882ec572cf0e5e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a>비갤러리 응용 프로그램에 대해 암호 Single Sign-On 구성 문제

이 문서가 도움이 되었나요 toounderstand hello 일반적인 문제 사람 얼굴을 구성할 때 **암호 single sign on** 갤러리 아닌 응용 프로그램입니다.

## <a name="how-toocapture-sign-in-fields-for-an-application"></a>어떻게 toocapture 로그인 응용 프로그램에 대 한 필드

로그인 필드 캡처는 HTML 기반 로그인 페이지에 대해서만 지원되고 Flash나 기타 비HTML 기반 기술을 사용하는 로그인 페이지처럼 **비표준 로그인 페이지에 대해서는 지원되지 않습니다.**

두 가지 방법으로 사용자 지정 응용 프로그램에 대한 로그인 필드를 캡처할 수 있습니다.

-   자동 로그인 필드 캡처

-   수동 로그인 필드 캡처

**자동 로그인 필드 캡처** 사용 하는 경우 대부분 HTML 기반 로그인 페이지를 사용 하 여 작동 **hello 사용자 이름 및 암호 입력에 대 한 잘 알려진 DIV Id** 필드입니다. 이 작동 하는 hello 방식 및 하는 hello 페이지 toofind 특정 조건과 일치 하는 DIV Id의 HTML 긁히는 hello 암호 tooit를 나중에 재생 수 있도록이 응용 프로그램에 대 한 메타 데이터를 저장 하십시오.

**수동 로그인 필드 캡처** 응용 프로그램 hello hello 사례에서 사용할 수 있습니다 **공급 업체 레이블이 표시 되지 않을** hello에 로그온 하는 데 사용 되는 필드를 입력 합니다. 수동 로그인 필드 캡처 hello 경우 hello 사용할 수도 있습니다 **여러 필드를 렌더링 하는 공급 업체** 자동으로 감지 될 수 없는 합니다. Azure AD 데이터를 저장할 수에 대 한 페이지에 서명 하는 hello에 만큼 필드 알려 주시면 hello 페이지에서 이러한 필드는 여기서으로 합니다.

일반적으로 **동안 hello 수동 옵션 자동 로그인 필드 캡처 작동 하지 않는 경우 항상 제안 합니다.**

### <a name="how-tooautomatically-capture-sign-in-fields-for-an-application"></a>Tooautomatically 응용 프로그램에 대 한 로그인 필드 캡처 방식

tooconfigure **암호 기반 Single sign-on** 사용 하 여 응용 프로그램에 대 한 **자동 로그인 필드 캡처**, 아래의 hello 단계를 수행 합니다.

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.

  * 여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**

6.  Tooconfigure single sign on 원하는 hello 응용 프로그램을 선택 합니다.

7.  Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.

8.  선택 hello 모드 **암호 기반 로그온 합니다.**

9.  Hello 입력 **로그온 URL**합니다. 사용자가을 자신의 사용자 이름 및 암호 toosign 입력할 수 있는 hello URL입니다. **Hello 로그인 필드를 제공 하는 hello URL에 표시 되는지 확인**합니다.

10. Hello 클릭 **저장** 단추입니다.

11. 이렇게 하면, 사용자 이름에 해당 URL 이벤트를 자동으로 처리 합니다 우리 및 암호 입력 상자 하 고 사용 하 되 면 toouse Azure AD toosecurely hello 액세스 패널 브라우저 확장을 사용 하 여 toothat 응용 프로그램 암호를 전송 합니다.

## <a name="how-toomanually-capture-sign-in-fields-for-an-application"></a>Toomanually 응용 프로그램에 대 한 로그인 필드 캡처 방식

toomanually 캡처 로그인 필드, 있어야 hello 액세스 패널 브라우저 확장을 설치 하 고 **inPrivate, incognito 또는 개인 모드에서 실행 되지 않습니다.** tooinstall hello 브라우저 확장을 hello에 hello 단계 수행 [어떻게 tooinstall hello 액세스 패널 브라우저 확장](#i-cannot-manually-detect-sign-in-fields-for-my-application) 섹션.

tooconfigure **암호 기반 Single sign-on** 사용 하 여 응용 프로그램에 대 한 **수동 로그인 필드 캡처**, 아래의 hello 단계를 수행 합니다.

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.

   * 여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**

6.  Tooconfigure single sign on 원하는 hello 응용 프로그램을 선택 합니다.

7.  Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.

8.  선택 hello 모드 **암호 기반 로그온 합니다.**

9.  Hello 입력 **로그온 URL**합니다. 사용자가을 자신의 사용자 이름 및 암호 toosign 입력할 수 있는 hello URL입니다. **Hello 로그인 필드를 제공 하는 hello URL에 표시 되는지 확인**합니다.

10. Hello 클릭 **저장** 단추입니다.

11. 이렇게 하면, 사용자 이름에 해당 URL 이벤트를 자동으로 처리 합니다 우리 및 암호 입력 상자 하 고 사용 하 되 면 toouse Azure AD toosecurely hello 액세스 패널 브라우저 확장을 사용 하 여 toothat 응용 프로그램 암호를 전송 합니다. 이 작업이 실패 하면 hello 경우에서 수 **변경 hello 로그인 모드 toouse 수동 로그인 필드 캡처** toostep 12 계속 여 합니다.

12. **&lt;앱 이름&gt; 암호 Single Sign-On 설정 구성**을 클릭합니다.

13. 선택 hello **로그인 필드를 수동으로 검색** 구성 옵션입니다.

14. **Ok**를 클릭합니다.

15. **Save**를 클릭합니다.

16. 화면 지침 toouse hello 액세스 패널에 hello를 따릅니다.

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a>“해당 URL에서 로그인 필드를 찾을 수 없습니다” 오류가 표시됨

로그인 필드 자동 검색에 실패하면 이 오류가 표시됩니다. hello에서 단계를 시도 수동 로그인 필드 검색 hello 수행 하 여이 문제는 tooresolve [toomanually 응용 프로그램에 대 한 로그인 필드 캡처 방식](#how-to-manually-capture-sign-in-fields-for-an-application) 섹션.

## <a name="i-see-an-unable-toosave-single-sign-on-configuration-error"></a>"없습니다 toosave Single Sign on 구성" 오류가 발생

드문 경우 이지만 특정 hello single sign on 구성 업데이트가 실패할 수 있습니다. tooresolve이 구성을 저장 하는 hello single sign on 다시 시도 하십시오.

Toofail를 일관 되 게 계속 열고 지원 케이스 정보를 제공 hello hello에 수집 된 [어떻게 toosee hello 세부 정보는 포털 알림](#i-cannot-manually-detect-sign-in-fields-for-my-application) 및 [tooget 알림 세부 정보 tooa 전송 하 여 도움말 하는 방법 지원 엔지니어가](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) 섹션.

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a>응용 프로그램에 대한 로그인 필드를 수동으로 검색할 수 없음

일부 hello 동작 수동 검색이 작동 하지 않는 경우 표시 될 수는 다음과 같습니다.

-   hello 수동 캡처 프로세스가 toowork, 나타나지만 캡처된 hello 필드가 잘못 되었습니다.

-   hello 캡처 프로세스를 수행할 때 hello 오른쪽 필드 강조 표시 된 가져오기 안 함

-   hello 캡처 프로세스가 me toohello 응용 프로그램의 로그인 페이지 예상 대로 걸리지만 아무 일도 발생

-   수동 캡처 toowork, 나타나지만 SSO 내 사용자가 액세스 패널 hello에서 toohello 응용 프로그램을 이동할 때 발생 하지 않습니다.

이러한 문제가 발생 하는 경우 hello 다음을 확인 합니다.

-   Hello 최신 버전의 hello 액세스 패널 브라우저 확장이 있는지 확인 하십시오. **설치** 및 **활성화** hello에 hello 단계에 따라 [tooinstall 액세스 패널 브라우저 hello 하는 방법 확장](#how-to-install-the-access-panel-browser-extension) 섹션.

-   Hello 캡처 프로세스에 브라우저 하는 동안 려 하지 않았는지 확인 하십시오. **incognito, inPrivate, 또는 개인 모드**합니다. 이러한 모드에는 hello 액세스 패널 확장이 지원 되지 않습니다.

-   사용자가 하는 동안 hello 액세스 패널에서 toohello 응용 프로그램에서 toosign 시도 하지 않는 확인 **incognito, inPrivate, 또는 개인 모드**합니다. 이러한 모드에는 hello 액세스 패널 확장이 지원 되지 않습니다.

-   Hello 수동 캡처 프로세스를 다시 시도 하세요 hello 올바른 필드 위에 빨간색 hello 표식 인지 확인 합니다.

-   Hello 수동 캡처 프로세스가 toohang, 하거나 hello 로그인 페이지에서 수행 하지는 않습니다 (경우 3 위에), 아무것도 hello 수동 캡처 프로세스가 다시 시도 합니다. 하지만 키를 눌러 hello hello 프로세스를 완료 한 후이 이번 **F12** tooopen 브라우저의 개발자 콘솔 단추입니다. 한 번 hello를 열고 **콘솔** 유형과 **window.location= "&lt;hello 앱을 구성할 때 지정한 url에 hello 기호를 입력&gt;"** 누릅니다  **입력**합니다. 이 강제 페이지 hello 캡처 프로세스를 종료 하 고 캡처한 hello 필드 저장 리디렉션합니다.

위 방법으로 해결되지 않는 경우 Microsoft에서 도와드릴 수 있습니다. 시도 하면 정보 뿐 아니라 hello hello에 수집 된 hello 세부 정보와 함께 지원 상담 [어떻게 toosee hello 세부 정보는 포털 알림](#i-cannot-manually-detect-sign-in-fields-for-my-application) 및 [tooget tooa 지원 알림 세부 정보를 전송 하 여 도움말 하는 방법 엔지니어](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) 섹션 (있는 경우).

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Tooinstall은 액세스 패널 브라우저 확장을 hello 하는 방법

아래의 hello 단계를 수행 하는 액세스 패널 브라우저 확장 tooinstall hello:

1.  열기 hello [액세스 패널](https://myapps.microsoft.com) hello 지원 되는 브라우저와로 로그인 중 하나에 **사용자** Azure AD에 있습니다.

2.  클릭는 **password SSO 응용 프로그램** hello 액세스 패널에에서 있습니다.

3.  Hello 프롬프트 묻는 tooinstall hello 소프트웨어에서 선택 **지금 설치**합니다.

4.  브라우저에 따라 toohello 방향이 지정 된 다운로드 링크 할 수 있습니다. **추가** hello 확장 tooyour 브라우저.

5.  브라우저를 요청 하면 선택 tooeither **사용** 또는 **허용** hello 확장 합니다.

6.  설치되면 브라우저 세션을 **다시 시작**합니다.

7.  Hello 액세스 패널에 로그인 하 고 참조 하면 **시작** password SSO 응용 프로그램입니다.

Hello 직접 링크 아래에서 Chrome 및 Firefox에 대 한 hello 확장을 다운로드할 수 있습니다.

-   [Chrome 액세스 패널 확장](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Firefox 액세스 패널 확장](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-toosee-hello-details-of-a-portal-notification"></a>어떻게 포털 알림의 toosee hello 세부 정보

다음 hello 단계를 수행 하 여 포털 알림에 대 한 hello 세부 정보를 확인할 수 있습니다.

1.  hello 클릭 **알림** hello hello Azure 포털의 오른쪽 위에 있는 아이콘 (hello 벨)

2.  에 모든 알림 선택는 **오류** 상태 (빨강 (!) 다음 toothem 순위가).

  >[!NOTE] **성공** 또는 **진행 중** 상태에서 알림을 클릭할 수 없습니다.
  >
  >

3.  이 열린 hello **알림 세부 정보** 블레이드입니다.

4.  사용 하 여이 정보 직접 toounderstand hello 문제에 대 한 세부 정보.

5.  여전히 도움이 필요 하거나, 문제에는 지원 엔지니어 또는 hello 제품 그룹 tooget 도움말와이 정보를도 공유할 수 있습니다.

6.  Hello 클릭 **복사** **아이콘** toohello hello의 오른쪽 **오류 복사** textbox toocopy 모든 hello 지원 또는 제품 그룹 엔지니어와 알림 세부 정보 tooshare 합니다.

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a>알림 세부 정보 tooa 지원 엔지니어 전송 하 여 tooget 도움말 하는 방법

공유 하는 것이 중요 **세부 정보 아래에 나열 된 모든 hello** 신속 하 게 이용할 수 있도록, 한 도움이 필요한 경우 지원 엔지니어와 합니다. 있습니다 수 간편 하 게 **는 스크린샷을 만든** hello를 클릭 하 여 **복사 오류 아이콘**, toohello 오른쪽 hello에 찾을 **오류 복사** 텍스트 상자에 붙여넣습니다.

## <a name="notification-details-explained"></a>알림 세부 정보 설명

아래 hello 의미 더 어떤 항목에는 각각 hello 알림 및 각각의 사용 예를 설명 합니다.

### <a name="essential-notification-items"></a>중요 알림 항목

-   **제목** – hello 알림 설명이 포함 된 제목을 hello

    -   예제 - **응용 프로그램 프록시 설정**

-   **설명** – hello에 대 한 hello 작업의 결과로 발생 한 문제 설명

    -   예제 - **입력한 내부 url은 이미 다른 응용 프로그램에서 사용 중입니다.**

-   **알림 Id** – hello hello 알림의 고유 id

    -   예제 – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**

-   **클라이언트 요청 Id** – 브라우저 수행한 hello 특정 요청 id

    -   예제 – **302fd775-3329-4670-a9f3-bea37004f0bc**

-   **스탬프의 UTC 시간** – hello는 hello 알림이 발생 한 utc에서 타임 스탬프

    -   예제 – **2017-03-23T19:50:43.7583681Z**

-   **내부 트랜잭션 Id** – hello toolook hello 오류 시스템에 사용 하는 내부 ID

    -   예제 – **71a2f329-ca29-402f-aa72-bc00a7aca603**

-   **UPN** – hello 작업을 수행한 hello 사용자

    -   예제 – **tperkins@f128.info**

-   **테 넌 트 Id** – hello 테 넌 트의 사용자 hello hello 작업을 수행한 hello 고유 ID는의 구성원

    -   예제 – **7918d4b5-0442-4a97-be2d-36f9f9962ece**

-   **사용자 개체 Id** – hello hello 작업을 수행한 hello 사용자의 고유 ID

    -   예제 – **17f84be4-51f8-483a-b533-383791227a99**

### <a name="detailed-notification-items"></a>자세한 알림 항목

-   **표시 이름** – **(비어 있을 수 있습니다)** hello 오류에 대 한 보다 자세한 표시 이름

    -   예* - **응용 프로그램 프록시 설정**

-   **상태** – hello hello 알림의 특정 상태

    -   예* – **실패**

-   **개체 Id** – **(비어 있을 수 있습니다)** 개체 ID는 hello에 대 한 작업을 수행한 hello

    -   예제 – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**

-   **세부 정보** – hello를 자세하게 hello 작업의 결과로 발생 한 문제 설명

    -   예제 – **내부 url 'http://bing.com/'은 이미 사용 중이므로 유효하지 않습니다.**

-   **오류 복사** – hello 클릭 **복사 아이콘** toohello hello의 오른쪽 **오류 복사** textbox toocopy 모든 지원 또는 제품 그룹 엔지니어와 알림 세부 정보 tooshare hello

    -   예 – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```

## <a name="next-steps"></a>다음 단계
[응용 프로그램 프록시 single sign on tooyour 앱을 제공 합니다.](active-directory-application-proxy-sso-using-kcd.md)

