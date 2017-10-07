---
title: "내 회사 또는 학교 계정에 대 한 2 단계 확인을 aaaSet | Microsoft Docs"
description: "회사에서 Azure Multi-factor Authentication을 구성 하는 경우 2 단계 인증에 대해 증명된 toosign 됩니다. 자세한 내용은 방법 tooset 설정 합니다. "
services: multi-factor-authentication
keywords: "어떻게 toouse azure 디렉터리를 active directory 자습서 hello 클라우드에서 active directory"
documentationcenter: 
author: kgremban
manager: femila
editor: pblachar
ms.assetid: 46f83a6a-dbdd-4375-8dc4-e7ea77c16357
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 69b04f74f6b28d0bcd94ca649b51092d9d139581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-my-account-for-two-step-verification"></a>2단계 인증에 내 계정 설정
2 단계 확인은 어려워지므로 다른 사람이 toobreak에 대 한 계정을 보호 하는 추가 보안 조치입니다. 이 문서를 읽고 있다면 아마도 회사 또는 학교 관리자로부터 Multi-Factor Authentication에 대한 전자 메일을 받았을 것입니다. 또는에서 toosign 시도 및 tooset 추가 보안 확인을 묻는 메시지가 표시 될 있습니다. 않은 hello 경우 **hello 자동 등록 프로세스 완료 될 때 까지는 로그인 할 수 없습니다**합니다.

이 문서를 통해 **회사 또는 학교 계정**을 설정할 수 있습니다. 고유의 개인 Microsoft 계정에 대 한 tooenable 2 단계 인증을 원하는 경우 참조 [2 단계 인증에 대 한](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification)합니다.

## <a name="set-up-your-account"></a>계정 설정

IT 부서는 2 단계 인증을 사용 하 여 toostart 해야, 라는 화면이 표시 됩니다 **관리자가 ड म ि न ा र이 ख 추가 보안 확인을 위해**:

![설정](./media/multi-factor-authentication-end-user-first-time/first.png)

시작 tooget 선택 **지금 설정 합니다.**

에 로그인 할 때 다음과 같은 화면이 표시 되지 않으면의 지시를 hello [2 단계 인증에 대 한 설정을 관리](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page) toofind hello 설정 페이지 확인 옵션을 관리할 수 있습니다. 

## <a name="decide-how-you-want-tooverify-your-sign-ins"></a>어떻게 결정 tooverify 로그인 속도가

hello 등록 프로세스의 첫 번째 질문 hello 방법 시겠습니까 toocontact가 있습니다. Hello 표에 hello 옵션 살펴보시기 바랍니다 하 고 각 메서드에 대 한 hello 링크 toogo toohello 설정 단계를 사용 합니다.

| 연락 방법 | 설명 |
| --- | --- |
| [모바일 앱](#use-a-mobile-app-as-the-contact-method) |- **확인 시 알림 수신.** 이 옵션 스마트폰 또는 태블릿에 알림 toohello authenticator 앱을 푸시합니다. Hello 알림을 본 합법적인 이면 선택 **Authenticate** hello 응용 프로그램에서 합니다. 회사 또는 학교에서는 인증 전에 PIN을 입력해야 할 수 있습니다.<br>- **확인 코드 사용.** 이 모드에서는 hello ऍ 30 초 마다 업데이트 하는 코드를 생성 합니다. Hello 로그인 인터페이스에 hello 최신 확인 코드를 입력 합니다.<br>hello Microsoft Authenticator 앱에 사용할 수 있는 [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), 및 [iOS](http://go.microsoft.com/fwlink/?Linkid=825073)합니다. |
| [휴대폰 통화 또는 문자](#use-your-mobile-phone-as-the-contact-method) |- **전화 통화** 제공 하는 자동화 된 음성 통화 toohello 전화 번호를 배치 합니다. Hello 통화 응답 hello 전화 키패드 tooauthenticate에 #를 누릅니다.<br>- **문자 메시지**는 확인 코드를 포함하는 문자 메시지를 보냅니다. Hello 텍스트에 hello 프롬프트에서 다음 toohello 문자 메시지에 회신 하거나 hello 로그인 인터페이스에 제공 된 hello 확인 코드를 입력 하십시오. |
| [사무실 전화 통화](#use-your-office-phone-as-the-contact-method) |제공 된 자동된으로 음성 통화 toohello 전화 번호를 배치 합니다. 응답 hello 호출 및 hello 전화 키패드 tooauthenticate 우물 정자 합니다. |

## <a name="use-a-mobile-app-as-hello-contact-method"></a>Hello 연락 방법으로 모바일 앱 사용
이 방법을 사용하려면 휴대폰이나 태블릿에 인증자 앱을 설치해야 합니다. hello 단계는이 문서의 내용에 기반 hello Microsoft Authenticator 앱에 사용할 수 있는 [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), 및 [iOS](http://go.microsoft.com/fwlink/?Linkid=825073)합니다.

1. 선택 **모바일 앱** hello 드롭 다운 목록에서 합니다.
2. **확인 시 알림 수신** 또는 **확인 코드 사용**을 선택한 후 **설정**을 선택합니다.

   ![추가 보안 확인 화면](./media/multi-factor-authentication-end-user-first-time/mobileapp.png)

3. 휴대폰 이나 태블릿에 hello 앱을 열고 선택  **+**  tooadd 계정. (선택 Android 장치에서 세 개의 점 다음 hello **계정 추가**.)
4. 회사 또는 학교 계정 tooadd 되도록 지정 합니다. 휴대폰의 hello QR 코드 스캐너가 열립니다. 카메라 제대로 작동 하지 않는 경우 있습니다 tooenter 회사 정보를 수동으로 선택할 수 있습니다. 자세한 내용은 [수동으로 계정 추가](#add-an-account-manually)를 참조하세요.  
5. Hello 모바일 앱 구성 hello 화면에 표시 된 hello QR 코드 그림을 스캔 합니다.  선택 **수행** tooclose hello QR 코드 화면입니다.  

   ![QR 코드 화면](./media/multi-factor-authentication-end-user-first-time/scan2.png)

6. 활성화 hello 전화를 마치면 선택 **연락처 me**합니다.  이 단계에 확인 코드 tooyour 휴대폰 또는 알림을 보냅니다. **확인**을 선택합니다.  
7. 회사에서 로그인 확인 인증 시 PIN이 필요한 경우 입력합니다.

   ![PIN 입력을 위한 상자](./media/multi-factor-authentication-end-user-first-time/scan3.png)

8. PIN 입력이 끝나면 **닫기**를 선택합니다. 이제 확인이 성공적으로 수행된 것입니다.
9. Access tooyour 모바일 앱을 손실 된 경우 휴대폰 번호를 입력 하는 것이 좋습니다. Hello 드롭 다운 목록에서 국가 지정 하 고 hello 상자 다음 toohello 국가 이름에 휴대폰 번호를 입력 합니다. **다음**을 선택합니다.
10. 이 시점에서 비 브라우저 앱 예: Outlook 2010 이상 또는 Apple 장치에서 기본 메일 앱 hello에 대 한 앱 암호를 입력 정보 요청된 tooset 됩니다. 일부 앱에서 2단계 인증을 지원하지 않기 때문입니다. 이러한 앱을 사용 하지 않으면 클릭 **수행** 고 hello 나머지 hello 단계를 건너뜁니다.
11. 이러한 앱을 사용 하는 hello 앱 암호 복사 제공 하 고 일반 암호 대신 응용 프로그램에 붙여 넣습니다. Hello에서는 여러 앱에 대 한 동일한 앱 암호입니다. 자세한 정보는 [앱 암호에 대한 도움말]을 참조하세요.
12. **Done**을 클릭합니다.

### <a name="add-an-account-manually"></a>수동으로 계정 추가
원하는 tooadd 계정 toohello 모바일 앱을 수동으로 hello QR 판독기를 사용 하는 대신 다음이 단계를 수행 합니다.

1. 선택 hello **계정을 수동으로 입력** 단추입니다.  
2. Hello에 동일한 페이지를 보여 주는 hello 바코드 제공 되는 hello 코드와 hello URL을 입력 합니다. 이 정보는 hello에 포함할지 **코드** 및 **URL** hello 모바일 앱에 있는 상자입니다.

    ![설정](./media/multi-factor-authentication-end-user-first-time/barcode2.png)
3. Hello 활성화 완료 되 면 선택 **연락처 me**합니다. 이 단계에 확인 코드 tooyour 휴대폰 또는 알림을 보냅니다. **확인**을 선택합니다.

## <a name="use-your-mobile-phone-as-hello-contact-method"></a>Hello 연락 방법으로 휴대폰 사용
1. 선택 **인증 전화** hello 드롭 다운 목록에서 합니다.  

    ![설정](./media/multi-factor-authentication-end-user-first-time/phone.png)  
2. Hello 드롭 다운 목록에서 국가 선택 하 고 휴대폰 번호를 입력 합니다.
3. 휴대폰에 전화-문자 또는 통화 toouse 방법을 hello 방법을 선택 합니다.
4. 선택 **연락처 me** tooverify 전화 번호입니다. 선택한 hello 모드에 따라 텍스트를 전송 우리 하거나 호출 합니다. Hello 화면에 제공 하는 hello 지침에 따라 다음 선택 **확인**합니다.
5. 이 시점에서 비 브라우저 앱 예: Outlook 2010 이상 또는 Apple 장치에서 기본 메일 앱 hello에 대 한 앱 암호를 입력 정보 요청된 tooset 됩니다. 일부 앱에서 2단계 인증을 지원하지 않기 때문입니다. 이러한 앱을 사용 하지 않으면 클릭 **수행** 고 hello 나머지 hello 단계를 건너뜁니다.
6. 이러한 앱을 사용 하는 hello 앱 암호 복사 제공 하 고 일반 암호 대신 응용 프로그램에 붙여 넣습니다. Hello에서는 여러 앱에 대 한 동일한 앱 암호입니다. 자세한 정보는 [앱 암호에 대한 도움말]을 참조하세요.
7. **Done**을 클릭합니다.

## <a name="use-your-office-phone-as-hello-contact-method"></a>Hello 연락 방법으로 사무실 전화 사용
1. 선택 **사무실 전화** hello 드롭다운 목록에서  

    ![설정](./media/multi-factor-authentication-end-user-first-time/office.png)  
2. hello 전화 번호 상자는 회사 연락처 정보 자동으로 채워집니다. Hello 번호가 잘못 되었거나 누락 된 경우 변경 내용을 toomake 관리자를 게 문의 합니다.
3. 선택 **연락처 me** tooverify 않으며 자신의 전화 번호를 호출 합니다 사용자의 번호입니다. Hello 화면에 제공 하는 hello 지침에 따라 다음 선택 **확인**합니다.
4. 이 시점에서 비 브라우저 앱 예: Outlook 2010 이상 또는 Apple 장치에서 기본 메일 앱 hello에 대 한 앱 암호를 입력 정보 요청된 tooset 됩니다. 일부 앱에서 2단계 인증을 지원하지 않기 때문입니다. 이러한 앱을 사용 하지 않으면 클릭 **수행** 고 hello 나머지 hello 단계를 건너뜁니다.
5. 이러한 앱을 사용 하는 hello 앱 암호 복사 제공 하 고 일반 암호 대신 응용 프로그램에 붙여 넣습니다. Hello에서는 여러 앱에 대 한 동일한 앱 암호입니다. 자세한 내용은 [앱 암호란 무엇인가요?](multi-factor-authentication-end-user-app-passwords.md)를 참조하세요.
6. **Done**을 클릭합니다.

## <a name="next-steps"></a>다음 단계
* 기본 옵션 변경 및 [2단계 인증을 위한 설정 관리](multi-factor-authentication-end-user-manage-settings.md)
* 2단계 인증을 지원하지 않는 네이티브 장치 앱에 대해 [앱 암호](multi-factor-authentication-end-user-app-passwords.md)를 설정합니다.
* 체크 아웃 hello [Microsoft Authenticator 앱](microsoft-authenticator-app-how-to.md) 셀 서비스 없는 경우에 보안 인증에 대 한 빠른, 합니다.
