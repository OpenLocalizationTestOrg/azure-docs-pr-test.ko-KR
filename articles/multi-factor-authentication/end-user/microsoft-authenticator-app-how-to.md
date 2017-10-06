---
title: "휴대폰에 대 한 aaaMicrosoft ऍ | Microsoft Docs"
description: "자세한 내용은 방법 tooupgrade toohello 최신 버전의 Azure Authenticator 합니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3065a1ee-f253-41f0-a68d-2bd84af5ffba
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: H1Hack27Feb2017, end-user
ms.openlocfilehash: d895d92d89613cbafd9fc09d4ff4810cbf25652e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-microsoft-authenticator-app"></a>Hello Microsoft Authenticator 앱 시작
hello Microsoft Authenticator 앱 추가 수준을 제공 하는 회사 또는 학교 계정에 보안 (예를 들어 bsimon@contoso.com) 또는 Microsoft 계정 (예를 들어 bsimon@outlook.com).

hello 앱 두 가지 방법 중 하나에서 작동합니다.

* **알림**. hello 앱 tooaccounts 무단된 액세스를 방지 하 고 알림 tooyour 스마트폰 또는 태블릿에 푸시하여 사기성 트랜잭션을 중지 데 도움이 됩니다. Hello 알림을 본 합법적인 이면 선택 **확인**합니다. 그렇지 않으면 **거부**를 선택합니다. 
* **확인 코드**. hello 앱을 소프트웨어 토큰 toogenerate OAuth 확인 코드 처럼 사용할 수 있습니다. 사용자 이름 및 암호를 입력 한 후 hello 로그인 화면에 hello 응용 프로그램에서 제공 하는 hello 코드를 입력 합니다. hello 확인 코드는 두 번째 형식의 인증을 제공합니다.

hello Microsoft Authenticator 앱 hello Azure Authenticator 앱을 대체합니다. hello Azure Authenticator 앱 작동 하지만 toomove toohello 새 Microsoft Authenticator 앱을 결정 한 경우이 문서는 고객을 지원 합니다.  

## <a name="opt-in-for-two-step-verification"></a>2단계 인증에 옵트인

hello Microsoft Authenticator 앱은 자체적으로 작동 하지 않습니다. 각 사용자 이름 및 암호를 사용 하 여 로그인 한 후 두 번째 확인 방법에 대 한 하 여 계정 tooprompt를 구성 합니다. 

회사 또는 학교 계정에 대 한 일반적으로 얻지 toochoose이이 기능은 자신에 대 한 합니다. 대신 보안 관리자가 사용자 대신 옵트인 하 고를 다음 계정에 대해 tooregister 확인 방법을 알립니다. 이 시나리오에 tooyou 적용 되는 경우에서 자세한 내용을 [무엇 Azure Multi-factor Authentication을 의미 합니까 내](multi-factor-authentication-end-user.md)합니다.

개인 계정으로 자신에 대 한 2 단계 확인을 tooset이 필요합니다. Microsoft 계정이 있는 경우 이러한 단계는 [2단계 인증 정보](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification)에서 사용할 수 있습니다. 

또한 Microsoft가 아닌 타사 계정으로 Microsoft Authenticator hello를 사용할 수 있습니다. Hello 기능 이외의 노드 2 단계 인증 호출 수 있지만 수 toofind 있어야 보안 또는 로그인 설정에서 합니다. 

## <a name="install-hello-app"></a>Hello 앱 설치
hello Microsoft Authenticator 앱에 사용할 수 있는 [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), 및 [iOS](http://go.microsoft.com/fwlink/?Linkid=825073)합니다.

## <a name="add-accounts-toohello-app"></a>계정을 toohello 앱 추가
Tooadd toohello Microsoft Authenticator 앱을 지정 하는 각 계정에 대해 다음 절차를 수행 하는 hello 중 하나를 사용 합니다.

### <a name="add-a-personal-microsoft-account-toohello-app"></a>개인 Microsoft 계정 toohello 앱 추가

개인 Microsoft 계정에 대 한 (하나 toosign를 사용 하는 등의 tooOutlook.com, Xbox, Skype,), 하면 toodo 됩니다 tooyour 계정 hello Microsoft Authenticator 앱에 로그인 합니다.

### <a name="add-a-work-or-school-account-toohello-app-using-hello-qr-code-scanner"></a>작업을 추가 또는 학교 계정 toohello hello QR 코드 스캐너를 사용 하 여 응용 프로그램
1. Toohello 보안 확인 설정 화면을 이동 합니다.  방법에 대 한 내용은 tooget toothis 화면 참조 [보안 설정 변경](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page)합니다.
2. 확인란 hello 다음 너무**Authenticator 앱** 다음 선택 **구성**합니다.

    ![hello 보안 확인 설정 화면에 hello 구성 단추](./media/authenticator-app-how-to/azureauthe.png)

    QR 코드가 있는 화면이 표시됩니다.

    ![Hello QR 코드를 제공 하는 화면](./media/authenticator-app-how-to/barcode2.png)
3. 열기 hello Microsoft Authenticator 앱입니다. Hello에 **계정** 화면에서  **+** , 한 다음 회사 또는 학교 계정 tooadd 되도록 지정 합니다.
4. Hello 카메라 tooscan hello QR 코드를 사용 하 여 선택한 후 **수행** tooclose hello QR 코드 화면입니다.

    카메라 제대로 작동 하지 않는 경우 다음을 할 수 있습니다 [hello QR 코드와 URL을 수동으로 입력](#add-an-account-to-the-app-manually)합니다.

5. Hello 응용 프로그램 아래에 6 자리 코드를 사용자 계정 이름에 표시 될 경우 작업이 끝났습니다. 

    ![계정 화면](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-manually"></a>계정 toohello 응용 프로그램을 수동으로 추가
1. Toohello 보안 확인 설정 화면을 이동 합니다.  방법에 대 한 내용은 tooget toothis 화면 참조 [보안 설정 변경](multi-factor-authentication-end-user-manage-settings.md)합니다.
2. **구성**을 선택합니다.

    ![hello 보안 확인 설정 화면에 hello 구성 단추](./media/authenticator-app-how-to/azureauthe.png)

    QR 코드가 있는 화면이 표시됩니다.  참고 hello 코드와 URL입니다.

    ![Hello QR 코드와 URL을 제공 하는 화면](./media/authenticator-app-how-to/barcode2.png)
3. 열기 hello Microsoft Authenticator 앱입니다. Hello에 **계정** 화면에서  **+** , 한 다음 회사 또는 학교 계정 tooadd 되도록 지정 합니다.

4. Hello 스캐너에서 선택 **코드를 수동으로 입력**합니다.

    ![QR 코드를 스캔하는 화면](./media/multi-factor-authentication-end-user-first-time/scan2.png)
5. Hello 코드와 URL hello hello hello 응용 프로그램에서 해당 상자에 입력 한 다음 선택 **마침**합니다.

    ![코드와 URL을 입력하기 위한 화면](./media/authenticator-app-how-to/manual.png)

6. Hello 응용 프로그램 아래에 6 자리 코드를 사용자 계정 이름에 표시 될 경우 작업이 끝났습니다.

    ![계정 화면](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-using-touch-id"></a>Touch ID를 사용 하 여 계정 toohello 앱 추가
iOS에서 hello Microsoft Authenticator 앱이 터치 ID 지원  Azure Multi-factor Authentication 조직 toorequire 장치에 대 한 PIN을 허용 합니다. Touch ID로, iOS 사용자는 PIN tooenter가 필요 하지 않습니다. 대신 지문을 스캔하고 **승인**을 선택할 수 있습니다.

Microsoft Authenticator를 통한 Touch ID 설정은 간단합니다. PIN을 사용하여 일반 확인 인증을 완료합니다. 장치에서 Touch ID를 지원하는 경우 Microsoft Authenticator는 자동으로 해당 계정에 대해 Touch ID를 설정합니다.

![Touch ID 설정 확인](./media/authenticator-app-how-to/touchid1.png)

때부터 앞으로 이동 했으면 사용자 로그인을 tooverify 필요한 푸시 알림을 수신 하는 hello를 선택 하 고 PIN을 입력 하는 대신 지문을 검색 합니다.

![푸시 알림](./media/authenticator-app-how-to/touchid2.png)

## <a name="use-hello-app-when-you-sign-in"></a>에 로그인 할 때 사용 하 여 hello 응용 프로그램

계정 toohello 응용 프로그램에 추가 되 면 모든 항목이 올바르게 구성 되어 있는지 테스트 확인 toomake 증명된 toodo 될 수 있습니다. 그런 다음 완료됩니다. 않아도 toodo 다른 항목이 hello 다음 번에 로그인 할 때까지 됩니다.

Toosee 시작 hello 응용 프로그램에서 확인 코드 toouse 했다면 hello 홈 페이지에서. 필요한 경우에 항상 새 코드를 갖도록 30초마다 변경됩니다. 하지만 필요는 없습니다 toodo 아무것도에 로그인 하 고 확인 코드 입력 정보 요청된 tooenter 됩니다 때까지 합니다.  
